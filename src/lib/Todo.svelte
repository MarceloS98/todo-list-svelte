<script>
  import { createEventDispatcher } from "svelte";

  export let content = "Placeholder text";

  const dispatch = createEventDispatcher();

  const dispatchEdit = () => dispatch("dispatchEdit", content);
  const dispatchDelete = () => dispatch("dispatchDelete", content);

  let done = false;
  const completeTodo = () => {
    done = !done;
  };
</script>

<div class="border-2 border-black flex items-center px-5 py-4 mb-1">
  <button
    on:click={completeTodo}
    class="border border-black w-5 h-5 rounded-full p-3 grid place-content-center"
  >
    {#if done}
      <i class="fa-solid fa-check" />
    {/if}
  </button>
  <p class="ml-3 text-lg" class:line-through={done}>{content}</p>
  <!-- Buttons container -->
  <div class="ml-auto text-xl">
    <button on:click={dispatchEdit}
      ><i class="mr-2 fa-solid fa-pen-to-square" /></button
    >
    <button on:click={dispatchDelete}><i class="fa-solid fa-trash" /></button>
  </div>
</div>
