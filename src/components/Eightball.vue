<template>
    <div class="eight-ball" @click="generateAnswer" :style="{ backgroundColor: color }">
        <p class="message">{{ message }}</p>
    </div>
    <button @click="resetEightBall">Reset</button>
    <div class="counts">
        <p>Green: {{ count.green }}</p>
        <p>Yellow: {{ count.goldenrod }}</p>
        <p>Red: {{ count.red }}</p>
    </div>
</template>
  
<script setup>
    import { ref, reactive } from 'vue';
    
    const props = defineProps({
        answers: Array
    });
    
    const color = ref('black');
    const message = ref('Think of a Question');
    const count = reactive({
        green: 0,
        goldenrod: 0,
        red: 0
    });
    
    const generateAnswer = () => {
        const randomAnswer = props.answers[Math.floor(Math.random() * props.answers.length)];
        color.value = randomAnswer.color;
        message.value = randomAnswer.msg;
        count[randomAnswer.color]++;
    };
    
    const resetEightBall = () => {
        color.value = 'black';
        message.value = 'Think of a Question';
    };
  </script>
  
  <style>
    .eight-ball {
        align-items: center;
        color: white;
        font-size: 20px;
        cursor: pointer;
        transition: background-color 0.5s ease;
        width: 300px;
        height: 300px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
    }

    button {
        margin-top: 20px;
    }
    
    .message {
        text-align: center;
        padding: 10px;
    }
</style>