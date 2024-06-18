<template>
  <div id="page">
    <h1 id="page-header">{{ pageHeader }}</h1>
    <div class="container">
      <p id="question">{{ currentQuestion }}</p>
      <button 
    v-for="(answer, index) in currentAnswers" 
    :key="index" 
    @click="handleButtonClick(answer, index)" 
    :class="{ 
        'correct-answer': index === correctAnswerIndex, 
        'incorrect-answer': index === incorrectAnswerIndex 
    }" 
    class="answer-button"
    :disabled="state.showNextButton"
    >
    {{ answer }}
</button>

    </div>
    <div id="go-next" v-if="state.showNextButton"> 
      <p id="next-t">{{ state.btnText }}</p>
      <img :src="nextBtn" id="next-btn" @click="nextQuestion">
    </div>
    <div v-if="state.showCongratulations" class="congratulations">כל הכבוד!</div>
    <div v-if="state.showBeGood" class="beGood">לא נורא </div>
    <div v-if="state.showPopUp" id="explain">
        <p id="pop-text">{{ explanation }}</p>
        <img id="closeBtn" :src="closeBtn" @click.once="closePopUP">
    </div>
    <div v-else>
        <p>No explanation available.</p>
    </div>
  </div>
</template>
<script setup>
import { defineProps, ref, reactive , defineEmits } from 'vue';
import nextBtn from "../assets/imgs/nextBtn.png";
import closeBtn from "../assets/imgs/closeBtn.png";

const props = defineProps({
  pageHeader: String,
  questions: Array,
  answers1: Array,
  answers2: Array,
  answers3: Array,
  correctAnswers: Array,
  explanations : Array
});

const emit = defineEmits(['go-next']);


const state = reactive({
  showNextButton: false,
  showCongratulations: false,
  showBeGood:false,
  showPopUp: false, 
  btnText: "שאלה הבאה",
});

const currentIndex = ref(0);
const correctAnswerIndex = ref(null);
const incorrectAnswerIndex=ref(null);
const currentQuestion = ref(props.questions[currentIndex.value]);
const explanation = ref(props.explanations[currentIndex.value]);
const currentAnswers = ref([
  props.answers1[currentIndex.value],
  props.answers2[currentIndex.value],
  props.answers3[currentIndex.value]
]);


const handleButtonClick = (answer, index) => {
  const correctAnswer = props.correctAnswers[currentIndex.value];
  if (answer === correctAnswer) {
    correctAnswerIndex.value = index;
    state.showNextButton = true;
    state.showCongratulations = true;
    state.showBeGood = false;
  } else {
    incorrectAnswerIndex.value = index;
    state.showCongratulations = false;
    state.showBeGood = true;
    setTimeout(()=>{
      state.showPopUp = true; 

    },2000)
  
  }
};

const nextQuestion = () => {
  if (currentIndex.value < props.questions.length - 1) {
    // השאלה אינה האחרונה
    currentIndex.value++;
    correctAnswerIndex.value = null;
    incorrectAnswerIndex.value = null;
    state.showNextButton = false;
    state.showCongratulations = false;
    state.showBeGood = false;
    currentQuestion.value = props.questions[currentIndex.value];
    currentAnswers.value = [
      props.answers1[currentIndex.value],
      props.answers2[currentIndex.value],
      props.answers3[currentIndex.value]
    ];
    state.btnText = "המשך"; 
  } else {
    emit('go-next');
  }
};



const closePopUP = () => {
    state.showPopUp = false;
    setTimeout(()=>{
        state.showNextButton = true;
    },500)
}
</script>

<style scoped>
@font-face { 
  font-family: "Heebo";
  src: url("../assets/fonts/Heebo-VariableFont_wght.woff"), 
  format("woff");

} 
.container {
  position: relative;
  top: 15vh;
  z-index: 0;
}

.answer-button {
  width: 90%;
  padding: 10px;
  margin-top: 3vh;
  background-color: rgb(31, 56, 100);
  color: white;
  border: none;
  border-radius: 7px;
  font-size: 1.3em;
  font-family: "Heebo";
  z-index: 0;

}

.correct-answer {
  background-color: rgb(34, 106, 91);
}

.incorrect-answer {
  background-color: rgb(220, 53, 69);
}

.congratulations {
  position: absolute;
  top: 105%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 2em;
  font-weight: bold;
  color: rgb(34, 106, 91);
  font-family: "Heebo";

}

.beGood{
 position: absolute;
  top: 105%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 2em;
  font-weight: bold;
  color: rgb(220, 53, 69);
  font-family: "Heebo";
}

#go-next {
  font-size: 1.3em;
  color: rgb(31, 56, 100);
  height: 10vh;
}

#next-btn {
  position: absolute;
  right: 45%;
  transform: rotate(2.5deg);
  top: 125%;
  animation: bounce2 2s ease infinite; /* Add animation delay */
  animation-delay: 15sec;
}

#next-t {
  position: absolute;
  right: 50%;
  transform: translateX(50%);
  top: 108%;
  font-weight: bold;
  
}

#explain {
  background-color: rgb(116, 142, 172);
  position: absolute;
  width: 92vw;
  height: 27vh; 
  z-index: 99999; 
  right: 50%;
  transform: translateX(50%);
  top:70%;
  text-align: center;
}
#pop-text{
  position: absolute;
  top: 20%;
  width: 80%;
  right: 50%;
  transform: translateX(50%);
  font-size: 1.2em;
  font-weight: bold;

}

#closeBtn{
    position: absolute;
    height:3vh;
    width: auto;
    right:8%;
    top:10%
}
#question {
  font-size: 1.4em; 
  font-family: "Heebo";
  color:  rgb(31, 56, 100);
  font-weight: bold;
  top:35vh;
  direction: rtl;
}
@keyframes bounce2 {
    0% {
      top: 125%;

    }
    50%{
      top: 135%;

    }
    100%{
      top: 125%;

    }
}

#page-header{
    position: absolute;
    top:8vh;
    right: 50%;
    transform: translateX(50%);
    font-size: 2em;
    width: 90vw;
    text-overflow: none;
    color:rgb(31,56,100);
}

</style>
