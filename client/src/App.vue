<script setup>
import WouldYouRather from './components/WouldYouRather.vue' //Links child element

import { ref, onMounted } from 'vue'
import wyrService from './services/wyrService'

const  wyrQuestion = ref('')
const wyrAnswer1 = ref('')
const wyrAnswer2 = ref('')

// this will store the user's answer once they make a choice

const userSelection = ref('')

onMounted( () => { //does something when program is displayed
  wyrService.getRandomWYR().then( (wyrData) => {
    //expect data to be something like 
    //{"question":"Have a cat-sized elephant or an elephant-sized cat?",
    //"answer1":"Cat-sized elephant",
    //"answer2":"Elephant-sized cat"}

    wyrQuestion.value = wyrData.question
    wyrAnswer1.value = wyrData.answer1
    wyrAnswer2.value = wyrData.answer2

  })
})

function updateUserSelection(userChoice){
  userSelection.value = `Thanks! You chose ${userChoice}`
}
</script>

<template>

  <div id="app-components">

    <h1>Hello! Would You Rather</h1>
    
    <!--V-bind sends data to the WYR child, v-on recieves data from WYR child-->
    <WouldYouRather 
    v-bind:question="wyrQuestion" 
    v-bind:answer1="wyrAnswer1"
    v-bind:answer2="wyrAnswer2"
    v-on:answer-selected="updateUserSelection" 
    ></WouldYouRather>

    <p>{{ userSelection }}</p>

</div>

</template>



<style scoped>
p {
  font-family:'Courier New', Courier, monospace;
}

#app-components{
  /*font-size: 3em;*/
  background-color: aqua;
  padding: 40px;
}

</style>
