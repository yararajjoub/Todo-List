<script>
// @ts-nocheck

    import Todo from "./Todo.svelte";

    export let todos = []
    export let activeEditTodo;

    $: activeTodos = activeEditTodo ? [activeEditTodo] : todos
</script>

<div class="todos-list">
    {#each todos as todo (todo.id) }

    <Todo {todo} {activeEditTodo} on:deleteTodo on:editTodo on:toggleTodo/>
    {/each}

  
</div>