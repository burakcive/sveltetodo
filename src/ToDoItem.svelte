<script>
  export let id;
  export let title;
  export let completed;

  
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";

  const dispatch = createEventDispatcher();

  const onComplete = () => {
    console.log("onComplete");

    if (completed) {
	  dispatch("onremove", id);
    } else {
      dispatch("oncomplete", id);
    }
  };


</script>


<style>
  li {
    cursor: pointer;
  }
  li:hover {
    color: gray;
  }
  .completed {
    text-decoration: line-through;
  }
</style>
{#if completed}
<li in:fly="{{ x: -600, duration: 500 }}" class:completed on:click={onComplete}>{title}</li>
{:else}
<li  class:completed on:click={onComplete}>{title}</li>
{/if}

