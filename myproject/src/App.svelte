<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte'
	let showModal = false;
	let Promo = false;
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

	const togglePromo = () => {
		Promo = !Promo
	}
	let num = 1;

	const addPerson = (e) => {
		const person = e.detail
		//... is a spread operator
		//place each object after the person 
		people = [person, ...people];
		showModal = false;
	}
</script>
	<!--gets the html from the modal component-->
	<Modal isPromo={Promo} {showModal} on:click={toggleModal}> 
		<!--this form now emits a custom event -->
		<AddPersonForm on:addPerson={addPerson}/>
	
	</Modal>
	<main>
		<button on:click={toggleModal}>Click Me</button>
		<button on:click={togglePromo}>Toggle Promo</button>
		{#each people as person (person.id)}
		  <div>
			<h4>{person.name}</h4>
			{#if person.beltColour === 'black'}
			  <p><strong>MASTER NINJA</strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColour} belt.</p>
			<button on:click={() => handleClick(person.id)}>Delete</button>
		  </div>
		{:else}
		  <p>There are no people to show...</p>
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