<!-- 27 -->
<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./reusableComps/Tabs.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";

  //tabs component:
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";

  const changeTab = (e) => {
    activeItem = e.detail;
  };

  let polls = [
    // dummy obj
    {
      id: 1,
      question: "Python or JavaScript?",
      answerA: "Python",
      answerB: "JavaScript",
      votesA: 9,
      votesB: 15,
    },
  ];

  const handleAdd = (e) => {
    const poll = e.detail;
    polls = [poll, ...polls];
    console.log(polls);
    activeItem = "Current Polls";
  };
</script>

<Header />
<main>
  <Tabs {activeItem} {items} on:changeTab={changeTab} />
  {#if activeItem === "Current Polls"}
    <PollList {polls} />
  {:else if activeItem === "Add New Poll"}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
