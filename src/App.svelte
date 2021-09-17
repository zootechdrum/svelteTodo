<script>
	import Todos from './components/Todos.svelte';
	let name = "user";
    let todos = [
        {id:1, name: 'create a Svelte starter app', completed:true},
        {id:2, name: 'Create your first component', completed:true},
        {id:3, name: 'Complete the rest of the tutorial', completed:false}
    ];
	function toggleName() {
		if(name === 'world') {
			name = 'svelte';
		} else {
			name = 'world';
		}
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<button on:click={toggleName}>Toggle name</button>
	<Todos todos={todos} />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>