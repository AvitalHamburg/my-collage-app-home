<template>
  <div id="page">
  <div v-if="!state.showGame">
   <h1 id="page-header"> בסיס פיקוד העורף   </h1>
   <div id="scroll-text">
    <p class="main-text" ref="text1">{{ emergencyText }}</p>
    <img class="image-content" :src="collageImg6" alt="Collage Image" ref="image1">
    <img class="image-content" :src="ImgCollage6" alt="Collage Image" ref="image2">
  </div>
  <div id="go-next">
   </div>
    <img :src="nextBtn" id="next-btn" @click="GoGame">
  </div>
    <Game></Game>

  </div>
  </template>

<script setup>
import { reactive, onMounted, getCurrentInstance ,defineEmits, ref} from 'vue';
import nextBtn from "../assets/imgs/nextBtn.png";
import collageImg6 from '../assets/imgs/collageImg6.jpg';
import ImgCollage6 from '../assets/imgs/6ImgCollage.jpg';
import Game from './Game.vue';
const emergencyText = `המכללה שלנו היא חלק ממערכת גדולה יותר , המפקדה של פיקוד העורף . היא כוללת הוצאה לאור לשכת אלוף פיקוד העורף . חדר אוכל של פיקוד העורף ובנוסף המאמ"פ שם ישנן מדריכות שליטה ובקרה שמדריכות על מערכת השועל שאחראית בין היתר על ההתראות לנפילת טילים. `
const emit = defineEmits(['go-menu']);

const state = reactive({ 
showGame:false
});


const GoGame = () => {
state.showGame=true;
};


const backToMenu = () =>{
    emit('go-menu');
}

const text1 = ref(null);
const image1 = ref(null);
const image2 = ref(null);

const handleIntersect = (entries, observer) => {
entries.forEach(entry => {
  if (entry.isIntersecting) {
    entry.target.classList.add('animate');
    observer.unobserve(entry.target);
  }
});
};

onMounted(() => {
const options = {
  root: null,
  rootMargin: '0px',
  threshold: 0.5,
};
const observer = new IntersectionObserver(handleIntersect, options);
observer.observe(text1.value);
observer.observe(image1.value);
observer.observe(image2.value);
});
</script>
<style scoped>
@font-face { 
  font-family: "Heebo";
  font-weight: normal;
  src: url("../assets/fonts/Heebo-VariableFont_wght.woff"), 
       format("woff");
}
#page {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  background-image: url("../assets/imgs/Bg2.png");
  background-size: cover;
  background-repeat: no-repeat;
  padding: 0;
  margin: 0;
  overflow-y: scroll;
}

#shape {
  position: absolute;
  left: 0;
  top: 0;
  height: 18vh;
}

#scroll-text {
  /* Adjust positioning and dimensions */
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  width: 90vw;
  direction: rtl;
  text-align: right;
}

#page-header {
  font-size: 2em;
  color: rgb(31, 56, 100);
  font-family: "Heebo";
  text-align: center;
  margin-top: 10vh;
}

#next-btn {
  position: absolute;
  top: 130vh;
  left: 50%;
  transform: translateX(-50%) rotate(2.5deg);
}

.main-text {
  font-size: 1.2em;
  margin-bottom: 5vh;
}

.image-content {
  width: 100%;
  height: auto;
  margin-bottom: 2vh;
}

.image-description {
  font-size: 1.2em;
  margin-bottom: 5vh;
}
.animate {
  animation: fadeIn 1s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
