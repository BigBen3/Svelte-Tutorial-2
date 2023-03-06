<script>
	import Modal from './Modal.svelte';
	
	let showModal = false;
  let people = [
	{name: 'yoshi', beltColor: 'black', age: 25, id: 1},
	{name: 'mario', beltColor: 'orange', age: 45, id: 2},
	{name: 'luigi', beltColor: 'black', age: 35, id: 3},
  ];
	const handleClick = (id) => {
		//so if they are equal it keeps checking if they are not equal it is false and it knows it found the right id and filters that person out of the array. 
		// by filtering them out it takes the user out
		//so if the id is not equal to the id the it is true but if it does and it false and it filters that false on out
		people = people.filter((person) => person.id != id) 
	}
	const toggleModal = () => {
		showModal = !showModal
	}
	let num = 1;
</script>
	<!--gets the html from the modal component-->
	<Modal message="I am a proper, value" isPromo={true} {showModal} on:click={toggleModal} />
	 <main>
		<button on:click|once={toggleModal}> Click me</button>
	<!--you have the person id at the end because adds a unique key element to each item in the array links the html template to the array object-->
    {#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColor === 'black'}
				<strong><p>Master ninja</p></strong>
			{/if}
			<!--we want it to send the id to the handle click but only when the butotn is click so if we just had then handle click it and pass in the parameter it would not be a reference anymore and would be called autmatically so we use an arrow funciton that says when you click it it calls the handle click with the person id-->
			<button on:click={() => handleClick(person.id)}>Delete</button>
		</div>
		{:else}
			<p>No people to show</p>
	{/each}


</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h4 {
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