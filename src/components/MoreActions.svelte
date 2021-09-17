<script>
    import {createEventDispatcher} from 'svelte';
    const dispatch = createEventDispatcher();
    
    let completed = true;

    const checkAll = () => {
        dispatch('checkAll', completed)
        completed = !complted
    }

    const removeCompleted = () => dispatch('removeCompleted');

</script>

<div class="btn-group">
    <button type="button" class="btn btn__primary" on:click={checkAll}> all</button>
    <button type="button" class="btn btn__primary" on:click={removeCompleted}>remove Completed</button>
</div>