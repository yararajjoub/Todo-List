<script>
    import {CircleIcon} from 'svelte-feather-icons'
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
    
    export let activeEditTodo;
    export let isFilter;

    let value = ''

    const handleAddTodo = ()=> {
        if(!value.trim()) {
            return}
        dispatch('addTodo', value.trim())
        value = ''
    }

    const editChange= ()=> { 
        if(activeEditTodo){
            value = activeEditTodo.title
        }
    }

    const handleFilter= ()=> { 
        dispatch('filter' )
    }

    $: activeEditTodo, editChange()


</script>

<div class="todos-form">
    <div class="todos-form_icon" class:active={isFilter} role="button" tabindex="0" on:click={handleFilter} on:keydown={(e) => {if (e.key === 'Enter') handleFilter()}} aria-label="Filter Todos">
        <CircleIcon />
    </div>
    <!--its the same value as the input -->
    <div class="todos-form_form">
        <input bind:value type="text" placeholder=" Lägg till ny todo..."/>
    </div>
   <div class="todos-form_submit" >
    <button class="btn" disabled={!value.trim()} on:click={handleAddTodo} >
        {
            activeEditTodo ? 
            'Edit' :
            'Spara'
        }
    
    </button>
</div>

</div>