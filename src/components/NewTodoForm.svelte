<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let title = "";
  function handleSubmit() {
    dispatch("add", title);
    title = "";
  }
</script>

<form
  class="NewTodoForm flex justify-center p-4 mt-6"
  on:submit|preventDefault={handleSubmit}>
  <div>
    <input
      required
      class="focus:outline-none h-12 text-black px-2 rounded-sm"
      placeholder="New Todo..."
      type="text"
      name="title"
      bind:value={title} />
  </div>
  <button
    class="border border-2 px-4 py-2 ml-2 rounded-sm hover:bg-red-400 uppercase
    focus:outline-none">
    Add todo
  </button>
</form>
