<script>
  import { Label, Select } from "flowbite-svelte";
  import { createEventDispatcher } from "svelte";
  import { enhance } from "$app/forms";

  const dispatch = createEventDispatcher();
  let temperature = 5;

  function generating() {
    dispatch("generating");
  }
  function doneGenerating(result) {
    dispatch("done-generating", result);
  }

  const topics = ["Work", "People", "Animals", "Food", "Television"].map(
    (name) => ({ value: name.toLowerCase(), name }),
  );
  let topic = topics[0].value;

  const tones = [
    "Friendly",
    "Witty",
    "Sarcastic",
    "Silly",
    "Dark",
    "Goofy",
  ].map((name) => ({ value: name.toLowerCase(), name }));
  let tone = tones[0].value;

  const kinds = ["Pun", "One-liner", "Knock-Knock", "Story"].map((name) => ({
    value: name.toLowerCase(),
    name,
  }));
  let kind = kinds[0].value;
</script>

<div>
  <h3 class="text-center text-xl font-medium text-gray-900">Joke Parameters</h3>
  <div class="grid grid-cols-3 mt-8 mb-8 gap-1">
    <div>
      <Label>
        Topic
        <Select
          selected={topic}
          class="mt-2"
          items={topics}
          bind:value={topic}
        />
      </Label>
    </div>
    <div>
      <Label>
        Tone
        <Select selected={tone} class="mt-2" items={tones} bind:value={tone} />
      </Label>
    </div>
    <div>
      <Label>
        Kind
        <Select selected={kind} class="mt-2" items={kinds} bind:value={kind} />
      </Label>
    </div>
  </div>

  <div class="relative mb-8">
    <Label>
      <p class="text-center">Randomness</p>
      <input
        list="tickmarks"
        type="range"
        min="0"
        max="10"
        step="1"
        bind:value={temperature}
        class="w-full h-2 bg-gray-200 rounded-md cursor-pointer"
      />
      <datalist id="tickmarks">
        <option value="0"></option>
        <option value="1"></option>
        <option value="2"></option>
        <option value="3"></option>
        <option value="4"></option>
        <option value="5"></option>
        <option value="6"></option>
        <option value="7"></option>
        <option value="8"></option>
        <option value="9"></option>
        <option value="10"></option>
      </datalist>
    </Label>
    <span class="text-sm text-gray-500 absolute start-0 -bottom-6">0</span>
    <span class="text-sm text-gray-500 absolute end-1 -bottom-6">1</span>
  </div>

  <div class="text-center">
    <form
      method="POST"
      action="?/generate"
      use:enhance={() => {
        generating();
        return async ({ result }) => {
          doneGenerating(result.data);
        };
      }}
    >
      <input name="topic" type="hidden" bind:value={topic} />
      <input name="tone" type="hidden" bind:value={tone} />
      <input name="kind" type="hidden" bind:value={kind} />
      <input name="temperature" type="hidden" bind:value={temperature} />
      <button
        type="submit"
        class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
        >Generate</button
      >
    </form>
  </div>
</div>
