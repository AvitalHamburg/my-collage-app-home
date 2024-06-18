<template>
  <div id="page">
    <div v-if="!state.showQuestion">
      <h1 id="page-header">קשרי חוץ</h1>
      <img :src="nextBtn" id="next-btn" @click="GoQuestion">
      <div id="scroll-text">
        <p class="main-text" ref="text1" :class="{ hidden: state.isText1Hidden }">{{ emergencyText }}</p>
        <img class="image-content" :src="collageImg4" alt="Collage Image" ref="image1" :class="{ hidden: state.isImage1Hidden }">
        <p class="image-description" ref="text2" :class="{ hidden: state.isText2Hidden }">{{ emergencyText2 }}</p>
        <img class="image-content" :src="ImgCollage4" alt="Collage Image" ref="image2" :class="{ hidden: state.isImage2Hidden }">
      </div>
    </div>
    <AmericanQ v-if="state.showQuestion" :pageHeader="pageHead" :questions="questionArray" :answers1="firstAns" :answers2="seconedAns"
    :answers3="thirdAns" :correctAnswers="correctAnsArr" :explantions="explainArr" @go-next="MenuBack"></AmericanQ>
  </div>
</template>


<script setup>
import AmericanQ from './AmericanQ.vue';
import nextBtn from "../assets/imgs/nextBtn.png";
import { reactive, defineEmits, ref, onMounted, onBeforeUnmount } from 'vue';
import collageImg4 from '../assets/imgs/collageImg4.png';
import ImgCollage4 from '../assets/imgs/4ImgCollage.jpg'

const emergencyText = `אנחנו לגמרי בינלאומיים!
ומארחים משלחות בעלי תפקידים בממשלות וצבאות מרחבי העולם, שרוצים ללמוד על חוסנה של מדינת ישראל והתמודדות מיטבית בשעת חירום.`;
const emergencyText2 = `כבר יצא לנו להיפגש עם ראשת FEMA )רח"ל האמריקאית), מב"ל הספרדית, נציגים ממשטרת שבדיה, קהילות יהודיות מרחבי העולם וגורמים נוספים, שבאים מכל היבשות לשמוע על קידום המוכנות ברשויות המקומיות, ההכשרות והאימונים - מכיתה י' ועד משרדי הממשלה.`;

const emit = defineEmits(['menu-back']);

const state = reactive({
  showPayment: false,
  showQuestion: false,
});

const pageHead = "קשרי חוץ";
const questionArray = ['מי היה אצלנו?'];
const firstAns = ['שוודיה , ארה"ב , ספרד'];
const seconedAns = ['אנגליה , ארה"ב , יוון'];
const thirdAns = ['איטליה , ארה"ב'];
const correctAnsArr = ['שוודיה , ארה"ב , ספרד'];
const explainArr = ['המדינות שביקרו אצלנו הן : ארה"ב ספרד ושוודיה'];

const GoQuestion = () => {
  state.showQuestion = true;
};

const MenuBack = () => {
  emit('menu-back');
};

const text1 = ref(null);
const text2 = ref(null);
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
  observer.observe(text2.value);
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

@font-face { 
  font-family: "Heebo-Black";
  font-weight: normal;
  src: url("../assets/fonts/Heebo-Black.woff"), 
       format("woff");
}


#page {
position: fixed;
top: 0;
left: 0;
/* Adjust the height dynamically based on content */
height: 100vh;
width: 100vw;
/* background-image: url("../assets/imgs/Bg2.png"); */
background-color: aliceblue;
background-size: cover;
background-repeat: no-repeat;
padding: 0;
margin: 0;
overflow: auto; /* Add overflow to enable scrolling */
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
top: 15%;
left: 50%;
transform: translateX(-50%);
width: 90vw;
direction: rtl;
text-align: right;
height: 190vh;
}

#page-header {
font-size: 2em;
color: rgb(31, 56, 100);
font-family: "Heebo";
text-align: center;
margin-top: 10vh;
direction: rtl;
}



.titles-gray {
font-size: 2.5em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "karantina";
color: rgb(89,89,89);
}

.simple-text {
width: 100%;
height: auto;
margin-bottom: 2vh;
font-family: "Heebo";
font-size: 1.2em;

}

.blue-text {
font-size: 1.4em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color:rgb(28, 180, 227);
width: 95vw;
}
.grey-bold {
font-size: 1.3em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color: rgb(89,89,89);
}
.grey-big {
font-size: 2em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color: rgb(89,89,89);
}
.animate {
animation: fadeIn 1s ease;
}


@keyframes bounce2 {
  0% {
      top: 180vh; /* Adjusted initial position */
  }
  50%{
    top: 185vh; /* Adjusted midpoint position */
  }
  100%{
    top: 180vh; /* Adjusted final position */
  }
}

#next-wBtn{
position:absolute;
z-index: 5;
right:50%;
transform: translateX(50%);
top:150vh; /* Adjusted position */
animation: bounce2 2s ease infinite; 
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

.image-content {
width: 100%;
height: auto;
margin-bottom: 2vh;
}
</style>
