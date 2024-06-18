<template>
  <div id="page">
    <div v-if="!state.showInfo">
   <div id="scroll-text">
    <p class="titles-gray" ref="text1">פעילות המכללה</p>
    <p class="blue-text" ref="text2">ברוכים הבאים וברוכות הבאות למכללה הלאומית לאיתנות ישראלית</p>
    <p class="simple-text" ref="text3">המכללה מכשירה מנהלים ומנהלות שיש להם תפקיד בשעת חירום ממשרדי הממשלה, רשויות ייעודיות, הרשויות המקומיות ובמפקדות צבאיות, לתפקוד מיטבי וניהול מצבי חירום כמו במצב מלחמה, טרור, אסון טבע, אסון אזרחי, מגיפה ועוד.
    </p>
    <img class="image-content" :src="ImgCollage" alt="Collage Image" ref="image1">
    <p class="simple-text" ref="text4">המכללה הוקמה בכדי להוות בית להכשרות בתחום ניהול מצבי החירום. בניין אחד המרכז את כל מחלקות פקע"ר בשיתוף פעולה עם רשות החירום הלאומית (רח"ל).</p>
    <p class='blue-text'  ref="text5">למכללה ארבע מגמות:</p>
    <p class="grey-bold"  ref="text6">1. מגמת הכשרות</p>
    <p class="simple-text"  ref="text7">אחראית להכשיר מנהלים ומנהלות של המכלולים ברשויות המקומיות. </p>
    <p class="grey-bold" ref="text8">2. מגמת משרדי ממשלה</p>
    <p class="simple-text" ref="text9">מגמה בהובלת רח"ל, האחראית על הכשרת מנהלים ומנהלות במשרדים לחירום. </p>
    <p class="grey-bold" ref="text10">3. מגמת אימוני מפקדות</p>
    <p class="simple-text" ref="text11">הרגל הצבאית שלנו, מכשירה, מאמנת וחונכת את כל בעלי התפקידים במפקדה צבאית של פיקוד העורף. </p>
    <p class="grey-bold" ref="text12">4. מגמת אימוני רשויות</p>
    <p class="simple-text" ref="text13">אחראית לממש את מה שנלמד בהכשרה - באימון לפי תרחיש ועל-פי תוכנית מותאמת. </p>
    <!-- <img class="image-content" :src="ImgCollage1" alt="Collage Image" ref="image2"> -->

  </div>
  <img ref="nextB" :src="nextBtn" id="next-wBtn" @click="goToInfo">
</div>
  <knowInfo v-if="state.showInfo" @go-menu="goToMenu"></knowInfo>
  </div>
</template>

<script setup>
import { reactive, onMounted, getCurrentInstance ,defineEmits, ref} from 'vue';
import knowInfo from './knowInfo.vue';
import ImgCollage from '../assets/imgs/11ImgCollage.jpg';
import nextBtn from "../assets/imgs/nextBtn.png";


const emit = defineEmits(['go-menu']);

const state = reactive({ 
showInfo: false
});

const goToInfo = () => {
console.log(state.showInfo);
state.showInfo = true;
};

const goToMenu = () =>{
emit('go-menu');
}

const text1 = ref(null);
const text2 = ref(null);
const text3 = ref(null);
const text4 = ref(null);
const text5 = ref(null);
const text6 = ref(null);
const text7 = ref(null);
const text8 = ref(null);
const text9 = ref(null);
const text10 = ref(null);
const text11= ref(null);
const text12= ref(null);
const text13= ref(null);
const image1 = ref(null);
// const image2 = ref(null);
// const nextT = ref(null);
const nextB = ref(null);


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
observer.observe(text3.value);
observer.observe(text4.value);
observer.observe(text5.value);
observer.observe(text6.value);
observer.observe(text7.value);
observer.observe(text8.value);
observer.observe(text9.value);
observer.observe(text10.value);
observer.observe(text11.value);
observer.observe(text12.value);
observer.observe(text13.value);
observer.observe(image1.value);
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
color: rgb(89,89,89);
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