<script>
  import { createEventDispatcher } from "svelte";
  import Buttons from "../reusableComps/Buttons.svelte";

  let dispatch = createEventDispatcher();

  let fields = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };
  let valid = false;

  const submitHandler = () => {
    valid = true;
    //validate quest
    if (fields.question.trim().length < 5) {
      valid = false;
      errors.question = "Question must be at least 5 characters long.";
    } else {
      errors.question = "";
    }

    //validate ansA
    if (fields.answerA.trim().length < 1) {
      valid = false;
      errors.answerA = "Answer A cannot be empty.";
    } else {
      errors.answerA = "";
    }

    //validate ansB
    if (fields.answerB.trim().length < 1) {
      valid = false;
      errors.answerB = "Answer B cannot be empty.";
    } else {
      errors.answerB = "";
    }

    //add new poll
    if (valid) {
      //compose new poll object
      let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
      //   console.log("Valid", fields);
      dispatch("add", poll);
    }
  };
</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-field">
    <label for="question">Poll question:</label>
    <input type="text" id="question" bind:value={fields.question} />
    <div class="error">{errors.question}</div>
  </div>

  <div class="form-field">
    <label for="answer-a">Answer A:</label>
    <input type="text" id="answer-a" bind:value={fields.answerA} />
    <div class="error">{errors.answerA}</div>
  </div>

  <div class="form-field">
    <label for="answer-b">Answer B:</label>
    <input type="text" id="answer-b" bind:value={fields.answerB} />
    <div class="error">{errors.answerB}</div>
  </div>

  <Buttons type="secondary" flat={true}>Add Poll</Buttons>
</form>

<style>
  form {
    width: 400px;
    margin: auto;
    text-align: center;
  }

  .form-field {
    margin: 18px auto;
  }

  input {
    width: 100%; /*100% of 400px*/
    border-radius: 6px;
  }

  label {
    margin: 10px auto;
    text-align: left;
  }

  .error {
    font-weight: bold;
    font-size: 12px;
    color: #d91b42;
  }
</style>
