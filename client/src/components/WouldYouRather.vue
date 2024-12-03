<script setup>
import { ref, watch } from 'vue'

defineProps({ //defines what is being sent from parent (App.Vue)
  question: String,
  answer1: String,
  answer2: String
}) 

const emit = defineEmits([  //Emits is what is sent back to parent 
  'answer-selected'
])

const choice = ref(null) //set to null so both choices arent automatically chosen

// function choiceMade() {
//   // emit event to tell parent that user has made choice.
//   emit('answer-selected', choice.value)
// }

watch(choice, () => {  //watches to see if value changes, if it does then it does what its told to do
  emit('answer-selected', choice.value)  //in this case, it updates whats being emited
})

</script>

<template>

  <div id="wyr">

    <h2>Make your choice</h2>

    <p>{{ question }}</p>

    <div>
      <input v-model="choice" v-bind:value="answer1"  type="radio" id="answer-1">
      <label for="answer-1">{{ answer1 }}</label>
      <input v-model="choice" v-bind:value="answer2"  type="radio" id="answer-2">
      <label for="answer-2">{{ answer2 }}</label>
    </div>

  </div>
</template>

<style scoped>
#wyr{
  background-color: hotpink;
}

p {
  font-family: fantasy;
}

</style>
