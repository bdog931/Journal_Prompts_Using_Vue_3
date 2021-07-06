<template>
  <div id="app">
    <h1>Welcome Brandon, today's prompt is: </h1>
    <h2 class="todaysPrompt">
      {{ JournalPrompts[promptIndex] }}
    </h2>
    <button @click="skip">
      <img src="./icons/arrow-right.svg" alt="skip-button">
    </button>
    <!-- <img src="./icons/arrow-left.svg" alt="go-back-to-previous-button"> -->
    <img src="./icons/trash-2.svg" alt="delete-button">
    <img src="./icons/plus-square.svg" alt="add-your-own-button">
    <br><br>
    <p id="todaysDate"></p>
    <textarea name="journalEntry" id="" cols="100" rows="35"></textarea>
    <br><br>
    <button id="submitJournalEntry">Submit</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  setup(){
    const JournalPrompts = [
    "What was the happiest thing that's happened to you in the past week?",
    "Where do you see yourself in 6 months?",
    "3",
    "4",
    "5",
    "6"
    ]

    let indexIgrabFrom = 0;
    let promptIndex = 0;

    //Returns successful attempt of a not in use index (as in not setting our current display)
    let notCurrentIndex = () => {
    let attempt = Math.floor(Math.random() * JournalPrompts.length);
    if(attempt === indexIgrabFrom){
        return(notCurrentIndex());
    }
    if(attempt != indexIgrabFrom){
        indexIgrabFrom = attempt;
        return(attempt);
    }
    }

    //Grabbing anything but what is currently being displayed
    let grabNotWhatWasJustPrompted = () => {
    if(JournalPrompts.length < 2){
        return("You are all out of altnerative prompts -- add prompt to correct this.");
    }
    let validIndex = notCurrentIndex();
    // let notOldDisplayingPrompt = JournalPrompts[validIndex];
    return(validIndex);
    }

    // let selectedPrompt = JournalPrompts[Math.floor(Math.random() * JournalPrompts.length)];

    //Skip Button
    // document.getElementById('skip').addEventListener('click', displayingPrompt => {
    // let newPrompt = grabNotWhatWasJustPrompted();
    // selectedPrompt = newPrompt;
    // document.getElementById('prompt').innerHTML = newPrompt;
    // })

    function skip() = {
      promptIndex = grabNotWhatWasJustPrompted();
      console.log('skip')
      // console.log("My selected prompt is " + selectedPrompt);
    }

    const selectedPrompt = JournalPrompts[promptIndex];

    return { JournalPrompts, selectedPrompt, skip, promptIndex }
  }
}
</script>

<style>
#app {
  margin-top: 60px;
  background-color: rgb(14, 4, 41);  
  text-align: center;
}

html{
    scroll-behavior: smooth;
}

body{
    background-color: rgb(14, 4, 41);
    color: white;
    text-align: center;
}

.todaysPrompt{
    font-style: italic;
}
</style>


