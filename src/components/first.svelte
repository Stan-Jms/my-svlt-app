<script>
    //Inspiré de : https://svelte.dev/repl/7eb8c1dd6cac414792b0edb53521ab49?version=3.20.1

    let newItem = '';
    let todoList = [];
	
	function addToList() {
		if(newItem != '') {
            todoList.push({Texte: newItem, Etat: false});
            todoList = todoList;
            newItem = '';
        }
	}

	function removeFromList(i) {
		todoList.splice(i, 1)
		todoList = todoList;
    }
</script>
<h1>TodoList Component</h1>
<input bind:value={newItem} type="text" placeholder="Votre tâche à ajouter">
<button on:click={addToList}>Ajouter</button>

<br/>
{#each todoList as item, i}
	<input bind:checked={item.Etat} type="checkbox">
	<span class:checked={item.Etat}>{item.Texte}</span>
	<span on:click={() => removeFromList(i)}>❌</span>
	<br/>
{/each} 

<style>

</style>