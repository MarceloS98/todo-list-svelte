<script>
  import { createEventDispatcher } from "svelte";
  import { onMount } from "svelte";

  const dispatch = createEventDispatcher();

  export let inputValue;
  export let editMode;
  export let input;

  const dispatchAdd = () => {
    dispatch("dispatchInputValue", inputValue);
  };

  const dispatchInput = () => {
    dispatch("dispatchInput", input);
  };

  onMount(() => {
    dispatchInput();
  });
</script>

<form>
  <div class="border-2 border-black flex items-center p-3 mb-3">
    <input
      bind:value={inputValue}
      bind:this={input}
      type="text"
      placeholder="Ingresa un todo"
      class="w-full mx-3 px-1 py-2 "
    />
    {#if editMode}
      <input
        on:click|preventDefault
        type="submit"
        value="Guardar"
        class="bg-black text-white font-bold px-4 py-2 rounded-md ml-auto"
      />
    {:else}
      <input
        on:click|preventDefault={dispatchAdd}
        on:click={() => {
          inputValue = "";
        }}
        type="submit"
        value="Agregar"
        class="bg-black text-white font-bold px-4 py-2 rounded-md ml-auto"
      />
    {/if}
  </div>
</form>
