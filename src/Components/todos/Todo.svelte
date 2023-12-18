<script>
    import {CircleIcon, EditIcon, Trash2Icon} from 'svelte-feather-icons'
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
  
    export let todo;
    export let activeEditTodo;

    const hanldeDelete = () => {
        dispatch('deleteTodo', todo.id)
    }
    const hanldeEdit = () => {
        dispatch('editTodo', todo)
    }

    const handleToggleTodo = () => { 
        dispatch('toggleTodo', todo.id)}

</script>


<div class="todos-todo" class:done={todo.done} >
    
<div class="todos-todo_icon"
    on:click={handleToggleTodo}
    role="button"
    tabindex="0"
    on:keydown={(e) => {if (e.key === 'Enter') handleToggleTodo()}}
    aria-label="Toggle Todo">
    <CircleIcon/>
</div>



    <div class="todos-todo_text"> {todo.title} </div>
    
    {#if !activeEditTodo}
    <div class="todos-todo_cta">
       <div class="todos-todo_cta-edit"
            on:click={hanldeEdit}
            on:keydown={(e) => {if (e.key === 'Enter') hanldeEdit()}}
            role="button"
            tabindex="0"
            aria-label="Edit Todo">
           <EditIcon size="20" />
       </div>
     
       <div class="todos-todo_cta-delete"
            on:click={hanldeDelete}
            on:keydown={(e) => {if (e.key === 'Enter') hanldeDelete()}}
            role="button"
            tabindex="0"
            aria-label="Delete Todo">
           <Trash2Icon size="20" />
       </div>
   </div>
   {/if}
   
</div>