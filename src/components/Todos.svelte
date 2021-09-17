<script>
    import FilterButton from './FilterButton.svelte';
    import Todo from './Todo.svelte';
    import MoreActions from './MoreActions.svelte';

    export let todos = [];


    $:  totalTodos = todos.length;
    $:  completedTodos = todos.filter(todo => todo.completed).length;

    let newTodoName = '';


    function removeTodo(todo) {
        todos = todos.filter(t => t.id !== todo.id);
    }

    function addTodo() {
        todos = [...todos, {id: newTodoId, name: newTodoName, completed: false}];
        newTodoName = '';
    }

    let newTodoId
        $: {
            if (totalTodos = 0) {
                newTodoName = 1;
            } else {
                newTodoId = Math.max(...todos.map(t => t.id)) + 1;
            }
        }
    
    let filter = 'all'
        const filterTodos = (filter, todos) =>
            filter === 'active' ? todos.filter(t => !t.completed) :
            filter === 'complted' ? todos.filter(t => t.completed) :
            todos;

    function updateTodo(todo) {
      const i = todos.findIndex(t => t.id === todo.id)
      todos[i] = {...todos[i], ...todo}; 
    }

    const checkAllTodos = (completed) => todos.forEach(t => t.completed = completed);
    const removeCompletedTodos = () => todos = todos.filter(t => !t.completed);
</script>


<h1>Svelte To-Do list</h1><!-- Todos.svelte -->
<div class="todoapp stack-large">

    <img height="32" width='88' src="https://www.w3.org/WAI/wcag2A" alt="">

  <!-- NewTodo -->
  <form on:submit|preventDefault={addTodo}>
    <h2 class="label-wrapper">
      <label for="todo-0"  class="label__lg">
        What needs to be done?
      </label>
    </h2>
    <input type="text" id="todo-0" autocomplete="off"
      class="input input__lg" bind:value={newTodoName} />
    <button type="submit" disabled="" class="btn btn__primary btn__lg">
      Add
    </button>
  </form>

  <!-- Filter -->

  <FilterButton bind:filter={filter} />
  <!-- TodosStatus -->
  <h2 id="list-heading">{completedTodos} out of {totalTodos} items complted</h2>

  <!-- Todos -->
<ul role="list" class="todo-list stack-large" aria-labelledby="list-heading">
    {#each filterTodos(filter,todos) as todo (todo.id)}
        <li class="todo">
            <Todo {todo} on:remove={e => removeTodo(e.detail)} on:update={e => updateTodo(e.detail)}  />
        </li>
        {:else}
        <li>Nothing to do here</li>
    {/each}
</ul>

  <hr />

  <!-- MoreActions -->
<MoreActions
  on:checkAll={e => checkAllTodos(e.detail)}
  on:removeCompleted={removeCompletedTodos}
  />
</div>