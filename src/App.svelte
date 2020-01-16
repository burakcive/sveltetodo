<script>
  import ToDoItem from "./ToDoItem.svelte";
  import NewToDo from "./NewToDo.svelte";
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";

  let message = "ToDo app";
  let todos = [];

  onMount(async () => {
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/todos?userId=1`
    );
    todos = await res.json();
  });

  const completeTodo = e => {
    let todoToDeleteIndex = todos.findIndex(t => t.id === e.detail);

    todos[todoToDeleteIndex].completed = !todos[todoToDeleteIndex].completed;
    console.log(e.detail + " is deleted");
  };

  const addToDo = e => {
    let newTodo = e.detail;
    if (!newTodo) {
      alert("Check you item before adding.");
      return;
    }

    newTodo.id = todos.length + 1;
    todos = [...todos, newTodo];
  };

  const removeTodo = e => 
  {
	  todos = todos.filter(t => t.id !== e.detail);
  }

</script>

<style>
  ul {
    list-style-type: decimal;
  }

  .container {
    margin-top: 20px;
    padding-top: 20px;
    padding-bottom: 20px;
  }
</style>

<main class="container">
  <NewToDo on:onaddtodo={addToDo} />
  {#if todos.length == 0}
    <p>Loading</p>
  {:else}
    <div class="row">
      <div class="col">
        <ul>
          {#each todos.filter(t => !t.completed) as todo}
            <ToDoItem  on:onremove={removeTodo} on:oncomplete={completeTodo} {...todo} />
          {/each}
        </ul>
      </div>
      <div class="col">
        <ul>
          {#each todos.filter(t => t.completed) as todo}
            <ToDoItem on:onremove={removeTodo} on:oncomplete={completeTodo} {...todo} />
          {/each}
        </ul>
      </div>
    </div>
  {/if}
</main>
