<script setup>
  import { defineProps, defineEmits } from 'vue'

 const props = defineProps(["questions","questionsAnswered"]);
 const emit = defineEmits(["questionAnswered"]);

 const selectAnswere = (is_correct)=>{
    emit("questionAnswered",is_correct)
 }

</script>


<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
        ></div>
      <div class="status">
         {{ questionsAnswered }} out of {{ questions.length }} questions answered 
      </div>
    </div>
    <transition-group name="fade">

      <div class="single-question" v-for="(question, index) in questions" :key="index" v-show="questionsAnswered === index">

        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div class="answer" v-for="(answer, index) in question.answers" :key="index" @click="selectAnswere(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

