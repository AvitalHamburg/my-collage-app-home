<template>
  <div id="page">
    <div v-if="showResults" class="results-container">
      <p>סיימת את השאלון!</p>
      <p>הציון שלך הוא: {{ points }} / {{ maxPoints }}</p>
      <p>{{ feedbackMessage }}</p>
    </div>
    <div v-else class="container">
      <p id="question">{{ currentQuestion }}</p>
      <button 
        v-for="(answer, index) in currentAnswers" 
        :key="index" 
        @click="handleButtonClick(answer, index)" 
        :class="{
          'selected-answer': index === selectedAnswerIndex
        }"
        class="answer-button"
        :disabled="showResult"
      >
        {{ answer }}
      </button>
    </div>
    <div id="navigation-buttons">
      <button 
        id="prev-button"
        @click="prevQuestion"
        :disabled="currentIndex === 0"
      >
        שאלה קודמת
      </button>
      <button 
        id="next-button"
        @click="nextQuestion"
        :disabled="selectedAnswerIndex === null"
      >
        שאלה הבאה
      </button>
    </div>
    <div v-if="state.showPopUp" id="explain">
      <p id="pop-text">{{ explanation }}</p>
      <img id="closeBtn" :src="closeBtn" @click="closePopUP">
    </div>
    <div v-else>
      <p>No explanation available.</p>
    </div>
    <div v-if="pointsVisible">
      <p>נקודות: {{ points }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref, reactive } from 'vue';
import closeBtn from "../assets/imgs/closeBtn.png";

const props = defineProps({
  pageHeader: String,
  questions: Array,
  answers1: Array,
  answers2: Array,
  answers3: Array,
  answers4: Array,
  correctAnswers: Array,
  explanations: Array
});

const state = reactive({
  showPopUp: false,
});

const currentIndex = ref(0);
const points = ref(0);
const maxPoints = props.questions.length * 10;
const currentQuestion = ref(props.questions[currentIndex.value]);
const explanation = ref(props.explanations[currentIndex.value]);
const currentAnswers = ref([
  props.answers1[currentIndex.value],
  props.answers2[currentIndex.value],
  props.answers3[currentIndex.value],
  props.answers4[currentIndex.value]
]);

const selectedAnswerIndex = ref(null);
const showResults = ref(false);
const feedbackMessage = ref("");

const handleButtonClick = (answer, index) => {
  selectedAnswerIndex.value = index;
  const correctAnswer = props.correctAnswers[currentIndex.value];

  if (answer === correctAnswer) {
    points.value += 10;
  }
};

const updateQuestionData = () => {
  currentQuestion.value = props.questions[currentIndex.value];
  currentAnswers.value = [
    props.answers1[currentIndex.value],
    props.answers2[currentIndex.value],
    props.answers3[currentIndex.value],
    props.answers4[currentIndex.value]
  ];
  explanation.value = props.explanations[currentIndex.value];
  selectedAnswerIndex.value = null;
};

const nextQuestion = () => {
  if (currentIndex.value < props.questions.length - 1) {
    currentIndex.value++;
    updateQuestionData();
  } else {
    showResults.value = true;
    if (points.value >= 70) {
      feedbackMessage.value = "כל הכבוד! עברת את השאלון!";
    } else {
      feedbackMessage.value = "לא נורא, נסה שוב!";
    }
  }
};

const prevQuestion = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
    updateQuestionData();
  }
};

const closePopUP = () => {
  state.showPopUp = false;
};

const pointsVisible = ref(false); // Controls visibility of points
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

.results-container {
  position: relative;
  top: 15vh;
  text-align: center;
  font-size: 1.5em;
  color: rgb(31, 56, 100);
  font-family: "Heebo";
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

.selected-answer {
  background-color: rgb(116, 142, 172);
}

#navigation-buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
  position: absolute;
  bottom: 5vh; /* Place at the bottom */
  width: 90%;
  left: 50%;
  transform: translateX(-50%);
}

#prev-button,
#next-button {
  background-color: rgb(31, 56, 100);
  color: white;
  border: none;
  border-radius: 7px;
  padding: 10px 20px;
  font-size: 1.2em;
  font-family: "Heebo";
}

#prev-button:disabled,
#next-button:disabled {
  background-color: grey;
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

#pop-text {
  position: absolute;
  top: 20%;
  width: 80%;
  right: 50%;
  transform: translateX(50%);
  font-size: 1.2em;
  font-weight: bold;
}

#closeBtn {
  position: absolute;
  height:3vh;
  width: auto;
  right:8%;
  top:10%;
}

#question {
  font-size: 1.4em; 
  font-family: "Heebo";
  color: rgb(31, 56, 100);
  font-weight: bold;
  top:35vh;
  direction: rtl;
}

#page-header {
  position: absolute;
  top:8vh;
  right: 50%;
  transform: translateX(50%);
  font-size: 2em;
  width: 90vw;
  text-overflow: none;
  color: rgb(31, 56, 100);
}
</style>
