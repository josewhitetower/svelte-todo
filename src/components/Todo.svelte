<script>
  export let todo;
  import FaRegTrashAlt from 'svelte-icons/fa/FaRegTrashAlt.svelte'
  import FaRegEdit from 'svelte-icons/fa/FaRegEdit.svelte'
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let isEditing = false;
  let title = todo.title;
  function handleTitleClick(params) {
    dispatch("toggle");
  }
  function handleEditTodo(params) {
    isEditing = true;
  }
  function handleRemove(params) {
    dispatch("remove");
  }
  function handleSubmit(params) {
    isEditing = false;
    dispatch("edit", title);
  }
</script>

<div class="Todo bg-red-400 p-4 mb-2 text-left font-semibold hover:bg-red-300">

  {#if !isEditing}
    <div class="flex justify-between items-center">
      <p
        class={todo.isDone ? 'line-through' : null}
        on:click={handleTitleClick}>
        {todo.title}
      </p>
      <div class="flex">
        <span class="w-4 cursor-pointer" on:click={handleEditTodo}>
          <FaRegEdit />
        </span>
        <span class="w-4 cursor-pointer ml-2" on:click={handleRemove}>
          <FaRegTrashAlt />
        </span>
      </div>
    </div>
  {:else}
    <form on:submit|preventDefault={handleSubmit} class="text-center">
      <input
        class="focus:outline-none bg-red-400 font-semibold"
        type="text"
        bind:value={title} />
    </form>
  {/if}

</div>
