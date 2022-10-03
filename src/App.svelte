<script>
  import Input from "./lib/Input.svelte";
  import Todo from "./lib/Todo.svelte";

  let todoItems = ["Tarea 1", "Tarea 2", "Tarea 3", "Tarea 4"];
  let input;
  let inputValue = "";
  let editMode = false;
  let todoValueIndex;

  // Recibe el valor del componente input y si no está vacío, lo agrega a la lista de todoItems
  function addTodo(event) {
    if (event.detail === "") return;
    todoItems.push(event.detail);
    todoItems = todoItems;
  }

  // Recibe el elemento input para poder trabajar con el focus
  const getInput = (e) => {
    input = e.detail;
  };

  // Filtra todos los elementos que no coincidan con el contenido del todo targeteado
  const handleDelete = (e) => {
    todoItems = todoItems.filter((todoItem) => todoItem != e.detail);
  };

  // Guarda el index del valor de la lista de todos que coincide con el valor recibido con el dispatcher, el contenido recibido por el dispatcher
  // se pone como valor del input, el editmode se pone true para que cambie de boton y se focusea el input para mejor experiencia de usuario
  const handleEdit = (e) => {
    todoValueIndex = todoItems.indexOf(e.detail);
    inputValue = e.detail;
    editMode = true;
    input.focus();
  };

  // Se reemplaza el valor de la lista con el index guardado en la funcion previa con el nuevo valor del input, se limpia el input,
  // se cambia de boton y se le quita el focus al input
  const handleEditMode = (e) => {
    todoItems[todoValueIndex] = inputValue;
    inputValue = "";
    editMode = false;
    input.blur();
  };
</script>

<!-- Container -->
<main class="max-w-xl mx-auto">
  <h1 class="text-3xl font-bold uppercase text-center mt-10 mb-5">Todo list</h1>
  <Input
    on:dispatchInputValue={addTodo}
    on:dispatchInput={getInput}
    on:click={handleEditMode}
    bind:inputValue
    {editMode}
    {input}
  />
  <!-- Todos container -->
  <div>
    {#each todoItems as item}
      <Todo
        content={item}
        on:click={handleDelete}
        on:dispatchEdit={handleEdit}
        on:dispatchDelete={handleDelete}
      />
    {/each}
  </div>
  <!-- Todo list end -->
</main>
