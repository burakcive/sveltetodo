<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	
	const onAdd = () => {
		console.log("onAdd", newTodo);

		dispatch("onaddtodo", newTodo);

		newTodo = {
			title: ""
		}
	}

	let newTodo = {
		title:  ""
	}

</script>


<div class="input-group mb-3">
  <input bind:value={newTodo.title} type="text" class="form-control" placeholder="What do you need to accomplish?" aria-label="What do you need to accomplish?" 
  aria-describedby="button-addon2">
  <div class="input-group-append">
    <button on:click={onAdd} class="btn btn-secondary" type="button">Add Note</button>
  </div>
</div>
