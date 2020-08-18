<script>
  let picked = "all";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  function handleChange() {
    dispatch("picked", picked);
  }
</script>

<div class="flex justify-end mt-4 pr-4 items-baseline">
  <input
    type="radio"
    id="all"
    value="all"
    bind:group={picked}
    on:change={handleChange}
    class="mr-2" />
  <label for="all">All</label>
  <input
    type="radio"
    id="done"
    value="done"
    bind:group={picked}
    on:change={handleChange}
    class="ml-8 mr-2" />
  <label for="done">Done</label>
  <input
    type="radio"
    id="undone"
    value="undone"
    bind:group={picked}
    on:change={handleChange}
    class="ml-8 mr-2" />
  <label for="undone">Undone</label>
</div>
