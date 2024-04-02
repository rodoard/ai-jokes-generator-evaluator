<script>
  import { enhance } from "$app/forms";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function doneEvaluating(result) {
    dispatch("done-evaluating", result);
  }

  export let joke,
    error,
    loading,
    prompt,
    assessment,
    evaluationError,
    temperature;

  let evaluationDone = false || assessment.length;
  let evaluating = false;
</script>

<div class="min-h-full grid place-content-center">
  <div>
    {#if loading}
      <p>Loading joke...</p>
    {:else if error}
      <p>Error: {error}</p>
    {:else if joke}
      <article class="prose">
        <p>{joke}</p>
      </article>
      <div class="text-center mt-8">
        {#if !evaluationDone}
          <form
            method="POST"
            action="?/evaluate"
            use:enhance={() => {
              evaluating = true;
              return async ({ result }) => {
                doneEvaluating(result.data);
                evaluating = false;
                evaluationDone = true;
              };
            }}
          >
            <input name="joke" type="hidden" bind:value={joke} />
            <input name="prompt" type="hidden" bind:value={prompt} />
            <input name="temperature" type="hidden" bind:value={temperature} />
            <button
              disabled={evaluating === true}
              type="submit"
              class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
              >Evaluate</button
            >
          </form>
        {:else if evaluationError}
          <div>Evalutation error: {evaluationError}</div>
        {:else}
          <p class="text-center font-semibold mb-4">Evaluation:</p>
          <article class="prose">
            <p>{assessment}</p>
          </article>
        {/if}
      </div>
    {/if}
  </div>
</div>
