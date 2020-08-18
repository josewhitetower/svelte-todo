<script>
  import Todo from "./Todo.svelte";
  import NewTodoForm from "./NewTodoForm.svelte";
  import FilterTodos from "./FilterTodos.svelte";
  import { onMount } from 'svelte';
  let todos = [];
  onMount(() => {
		todos = JSON.parse(localStorage.getItem("todos") || "[]")
	});
  let filter = "all";
  $: filteredTodos =
    filter === "done"
      ? todos.filter(todo => todo.isDone)
      : filter === "undone"
      ? todos.filter(todo => !todo.isDone)
      : todos;
  function removeTodo(todo) {
    todos = todos.filter(td => td.title != todo.title);
    save();
  }
  function toggleTodo(index) {
    todos[index].isDone = !todos[index].isDone;
    save();
  }
  function editTodo(index, event) {
    todos[index].title = event.detail;
    save();
  }
  function addNewTodo(event) {
    const isAlreadyAdded = todos.find(todo => todo.title === event.detail);
    if (!isAlreadyAdded) {
      todos = [...todos, { title: event.detail, isDone: false }];
      save();
    }
  }
  function onPicked(event) {
    filter = event.detail;
  }
  function save() {
    localStorage.setItem("todos", JSON.stringify(todos));
  }
</script>

<div
  class="TodoList py-8 bg-red-500 text-center text-white font-sans rounded mt-8
  shadow-2xl">
  <h1 class="text-3xl uppercase font-thin mb-4">Todo List!</h1>
  {#each filteredTodos as todo, index (todo)}
    <Todo
      {todo}
      on:remove={() => removeTodo(todo)}
      on:toggle={() => toggleTodo(index)}
      on:edit={event => editTodo(index, event)} />
  {/each}
  <NewTodoForm on:add={event => addNewTodo(event)} />
  <FilterTodos on:picked={event => onPicked(event)} />
</div>
