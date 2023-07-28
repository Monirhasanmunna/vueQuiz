<script setup>
import { ref,reactive } from 'vue'
import Questions from './components/Questions.vue'
import Result from './components/Result.vue'

const questionsAnswered = ref(0);
const rightAnswere      = ref(0);

let  questions= reactive([
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "Fish",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: false,
            },
            {
              text: "6",
              is_correct: true,
            },
            {
              text: "12",
              is_correct: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
    ]);

const questionAnswered = (is_correct)=>{
  if(is_correct == true){
    rightAnswere.value++
  }
  questionsAnswered.value++
}
      
let results=reactive([
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ]);

const reset = ()=>{
  questionsAnswered.value = 0
  rightAnswere.value  = 0

}
</script>

<template>
    <Questions
    v-if="questionsAnswered < questions.length"
    :questions="questions"
    :questionsAnswered = "questionsAnswered"
    :rightAnswere = "rightAnswere"
    @questionAnswered="questionAnswered"
    />

    <Result v-else :rightAnswere="rightAnswere" :results="results"/>

    <button v-show="questionsAnswered == questions.length" @click="reset()" type="button" class="reset-btn">Reset</button>
</template>

<style scoped>

</style>
