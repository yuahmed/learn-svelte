<!-- props used to pass arguments to components -->
<script>
  import Modal from "./Modal.svelte";
  import AddPesonForm from "./AddPesonForm.svelte";

  let showModal = false;
  const toggleModal = () => {
    showModal = !showModal;
  };

  //   let firstName = "Mud";
  //   let lastName = "Red";
  //   let beltColor = "black";

  //   //   a reactive value:
  //   $: fullName = `${firstName} ${lastName}`;

  //   const handleClick = () => {
  //     beltColor = "orange";
  //   };

  //   const handleInput = (e) => {
  //     //event parameter
  //     beltColor = e.target.value;
  //   };

  let people = [
    {
      name: "yoshi",
      beltColor: "black",
      age: 25,
      id: 1,
      skills: ["running", "sneaking"],
    },
    { name: "mario", beltColor: "orange", age: 45, id: 2, skills: ["running"] },
    { name: "luigi", beltColor: "brown", age: 35, id: 3, skills: ["fighting"] },
  ];

  const handleClick2 = (id) => {
    //deleting person from people dict
    people = people.filter((ele) => ele.id != id);
  };

  const addPerson = (e) => {
    //data saved in e.detail (log to see)
    const person = e.detail;
    // ... = spread operator
    //...people takes current value of people, spreads it to new array
    people = [person, ...people];
    showModal = false;
  };
</script>

<!-- html to render based off of conditional logic can go here -->
<!-- passing in a prop to the modal comp. slots better alt. -->
<Modal {showModal} isPromo={true} on:click={toggleModal}>
  <!-- <div slot="title">
    <h3>Add a New Person</h3>
  </div> -->
  <AddPesonForm on:addPerson={addPerson} />
</Modal>
<!-- <Modal message="Heyyyyy" isPromo={true}/>  -->

<main>
  <!-- <h1>Hello {fullName}!</h1>
  <p>{fullName} {beltColor} belt</p>
  <input type="text" bind:value={firstName} />
  <input type="text" bind:value={lastName} />
  <input type="text" bind:value={beltColor} /> -->
  <!-- statement above equals to: -->
  <!-- <input type="text" on:input={handleInput} value={beltColor}> -->

  <button on:click={toggleModal}>Open Modal</button>
  <!-- think: foreach loop in JS  -->
  <!-- assigning unique ID for dom mapping (data to dom elements)  -->

  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColor === "black"}
        <p><strong>Master Ninja</strong></p>
      {/if}
      <p>is {person.age} years old, has a {person.beltColor} belt.</p>
      <p><em>Skills include:</em></p>

      {#each person.skills as skill}
        <p>{skill}</p>
      {/each}
      <button on:click={() => handleClick2(person.id)}>delete</button>
    </div>
  {:else}
    <p>There are no people to show.</p>
  {/each}
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
