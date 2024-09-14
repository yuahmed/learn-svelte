<script>
  import { createEventDispatcher } from "svelte";

  //allows to dispatch custome event
  let dispatch = createEventDispatcher(); //todo: read up on
  let name;
  let beltColor;
  let age;
  //   let fighting = false;
  //   let running = false;
  //   let sneaking = false;

  let skills = [];

  const handleSubmit = () => {
    const person = {
      name,
      beltColor,
      age,
      skills,
      id: Math.random(), //not recommended.
    };

    //dispatches custom event , handled in app component
    dispatch("addPerson", person);
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder="name" bind:value={name} />
  <input type="number" placeholder="age" bind:value={age} />

  <label>Skills:</label>
  <!-- alternative: group attr; implemented -->
  <!-- <input type="checkbox" bind:checked={fighting}/>Fighting<br />
  <input type="checkbox" bind:checked={running}/>Running<br />
  <input type="checkbox" bind:checked={sneaking}/>Sneaking<br /> -->

  <input type="checkbox" bind:group={skills} value="fighting" />Fighting<br />
  <input type="checkbox" bind:group={skills} value="running" />Runniing<br />
  <input type="checkbox" bind:group={skills} value="sneaking" />Sneaking<br />

  <label>Belt Color:</label>
  <select bind:value={beltColor}>
    <option value="black">Black</option>
    <option value="yellow">Yellow</option>
    <option value="brown">Brown</option>
    <option value="white">White</option>
  </select>

  <!-- if click event to record form input, would be on the button-->
  <button>Add Person</button>
</form>

<style>
</style>
