<script>
  import JokeParameters from "$lib/components/JokeParameters.svelte";
  import JokeDisplay from "$lib/components/JokeDisplay.svelte";

  let temperature;
  let prompt;
  let evaluationError = "";
  let error = "";
  let joke = "";
  let loading = false;
  let assessment = "";

  async function generating() {
    loading = true;
    prompt = "";
    temperature = "";
    joke = "";
    error = "";
  }
  function doneGenerating(event) {
    const result = event.detail;
    if (result.joke) {
      joke = result.joke;
      temperature = result.temperature;
      prompt = result.prompt;
    } else {
      error = result.error.message;
    }
    loading = false;
  }
  function doneEvaluating(event) {
    const result = event.detail;

    if (result.error) {
      evaluationError = result.error.message;
    } else {
      joke = result.joke;
      assessment = result.assessment;
    }
  }
</script>

<main class="grid grid-cols-2 gap-4 mt-8 text-sm">
  <div
    class="p-4 min-h-80 border rounded-md border-slate-300 border-spacing-3 border-colo"
  >
    <JokeParameters
      on:done-generating={doneGenerating}
      on:generating={generating}
    />
  </div>
  <div class="p-4 border rounded-md border-slate-300">
    <JokeDisplay
      on:done-evaluating={doneEvaluating}
      {joke}
      {loading}
      {assessment}
      {evaluationError}
      {error}
      {temperature}
      {prompt}
    />
  </div>
</main>
