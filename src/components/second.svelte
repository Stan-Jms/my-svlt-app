<script>
	import { is_empty, loop_guard } from "svelte/internal";
	// Inspiré de : https://tailwindui.com/components/marketing/sections/cta-sections (simple center branded)
	
	

	const storage = localStorage;

	let newItem = {
		text:"",
		title:"",
		button:""
	};

	let baseText = {
		text:"Lorem, ipsum dolor sit amet consectetur adipisicing elit. Quasi aut voluptate sunt necessitatibus veritatis tenetur incidunt? Recusandae commodi dolor itaque! Iusto vero at saepe. Vero, similique? Soluta ratione illum reiciendis.",
		title:"A propos de nous",
		button:"Voir plus"
	};

	let inputValues = {
		text:"",
		title:"",
		button:""
	};

	const addItem = (save) => {
		switch (save){
			case true:
				inputValues = newItem;
				newItem = {text:"", title:"", button:""};
				inputValues = inputValues;
				storage.setItem("key",JSON.stringify(inputValues));
				break;
			default:
			inputValues = newItem;
			newItem = {text:"", title:"", button:""};
			inputValues = inputValues;
		}
	}

	const is_null = (params) => {

		let unloaded = JSON.parse(storage.getItem("key"))
		if(unloaded === null) {
			unloaded = baseText;
		}
		switch(params) {
			case "title":
				return unloaded.title;
			case "text":
				return unloaded.text;
			case "button":
				return unloaded.button;
			default:
				console.error("Impossible de compiler votre demande.");

		}
	}

	

</script>
<h1>En savoir plus component</h1>
<div>
	<div>
		<h1>{!is_empty(inputValues.title) ? inputValues.title : (!is_empty(is_null("title")) ? is_null("title") : baseText.title) }</h1>

		<p>{!is_empty(inputValues.text) ? inputValues.text : (!is_empty(is_null("text")) ? is_null("text") : baseText.text) }</p>

		<button>{!is_empty(inputValues.button) ? inputValues.button : (!is_empty(is_null("button")) ? is_null("button") : baseText.button) }</button>
	</div>

	<div>
		<input bind:value={newItem.title} type="text" placeholder="Votre Titre à ajouter">
		<textarea bind:value={newItem.text} type="text" placeholder="Votre Texte à ajouter"></textarea>
		<input bind:value={newItem.button} type="text" placeholder="Votre Bouton à ajouter">
		<button on:click={() => addItem()}>Ajouter</button>
		<button on:click={() => addItem(true)}>Ajouter et sauvegarder</button>
	</div>
</div>

<style>
	
</style>
