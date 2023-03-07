<script>
    import { createEventDispatcher } from 'svelte';


    let dispatch = createEventDispatcher();

    let name;
    let beltColor;
    let age;
    let skills = [];
    const handleSubmit = () => {
       const person = {
        //would be like name:  name but if both variables are the same you can just do name, so I did that for all the variables 
            name,
            beltColor, 
            age,
            skills, 
            id: Math.random() 
       }
       //it emits a custom event to the parent componenet which is the app.svelte so that we can add the person object to the person array. 
       dispatch('addPerson', person);
    
    }
</script>


<form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="name" bind:value={name}>
    <input type="number" placeholder="age" bind:value={age}>
    <label>Skills:</label>
    <input type="checkbox" bind:group={skills} value="fighting">fighting<br>
    <input type="checkbox" bind:group={skills} value="sneaking">sneaking<br>
    <input type="checkbox" bind:group={skills} value="running">running<br>
    <label>Belt Color:</label>
    <select bind:value={beltColor}>
        <option value="black">Black</option>
        <option value="orange">Orange</option>
        <option value="brown">Brown</option>
        <option value="white">White</option>
    </select>
    <button>Add Person</button>
</form>

<style>

</style>