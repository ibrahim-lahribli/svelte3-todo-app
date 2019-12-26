<script>
  import TodoItem from "./TodoItem";
  let newTodoTitle = "";
  let currentFilter = "all";
  let nextId = 4;

  let todos = [
    {
      id: 1,
      title: "My first todo",
      completed: false
    },
    {
      id: 2,
      title: "My second todo",
      completed: false
    },
    {
      id: 3,
      title: "My third todo",
      completed: false
    }
  ];

  function addTodo(event) {
    if (event.key === "enter") {
      todos = [
        ...todos,
        {
          id: nextId,
          completed: false,
          title: newTodoTitle
        }
      ];

      newTodoTitle = "";
      nextId = nextId + 1;
    }
  }
</script>

<div class="container">
  <a href="https://google.com" target="blank">
    <img src={'/img/test.png'} alt="svelte logo" class="logo" />
  </a>

  <h2>Svelte todo App</h2>
  <input
    type="text"
    class="todo-input"
    placeholder="insert todo item ..."
    bind:value={newTodoTitle}
    on:keydown={addTodo} />
  {#each filteredTodos as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleToggleComplete} />
    </div>
  {/each}
  <div class="inner-container">
    <div>
      <label>
        <input
          class="inner-container-input"
          type="checkbox"
          on:change={checkAllTodos} />
        Check All
      </label>
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <button
        on:click={() => updateFilter('all')}
        class:active={currentFilter === 'all'}>
        All
      </button>
      <button
        on:click={() => updateFilter('active')}
        class:active={currentFilter === 'active'}>
        Active
      </button>
      <button
        on:click={() => updateFilter('completed')}
        class:active={currentFilter === 'completed'}>
        Completed
      </button>

      <button on:click={clearCompleted}>Clear Completed</button>

    </div>
  </div>
</div>
