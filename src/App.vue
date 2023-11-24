<script setup>

import {ref, reactive} from 'vue';
import {questions} from './data/question'

function getResult(){
  let score = 0;
  questions.map(question =>{
    if(question.answer!=null){
      const answerId =  question.options.find((idd)=>question.answer === idd.id)
      if(answerId.isCorrect === true){
        score++;
      }
    }
  })

  return score;
} 

</script>

<template>
  
<p class="text-xl">Score: {{  getResult() }}</p>
    <!-- {{ questions }} -->
<div class="parentdiv mt-5" v-for="(question, index) in questions" :key="index">
  <p>{{ index+1 }} {{ question.question }}</p>
  <ul>
    <li v-for="(option, optionIndex) in question.options" :key="optionIndex">
      <input type="radio" :name="'question_' + index" class="me-2" :value="option.id" v-model="question.answer">{{ option.text }}
    </li>
  </ul>

</div>



 
</template>

<style scoped>
.parentdiv li{
  list-style-type: none;
}
</style>
