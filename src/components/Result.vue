<script setup>
import { defineProps,computed } from 'vue';

const props = defineProps(['results', 'rightAnswere'])



  
  let  resultIndex=computed(()=> {
      let index = 0;

      props.results.forEach((e, i) => {
        if (e.min <= props.rightAnswere && e.max >= props.rightAnswere) {
          index = i;
        }
      });

      return index;
    })
  

</script>

<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

