<template>
  <div id="page">
   <div v-if="!state.showGif" id="scroll-text">
    <p class="titles-gray" ref="text1">נכסים דיגיטליים של המכללה    </p>
    <p class="grey-bold" ref="text2">המכללה עברה בשנתיים האחרונות טרנספורמציה דיגיטלית, עם הנגשה משמעותית של ידע בשעת חירום לצד שיפור תהליכים בשגרה, שהפכו קלים, קצרים ומהירים יותר.
    </p>
    <img class="image-content" :src="comp">
    <p class="blue-text">ידע ומידע - הכל באתר המכללה</p>
    <p class="simple-text">באתר המכללה ניתן להירשם ולקבל מידע על כל ההכשרות שלנו לבעלי תפקידים במשרדי הממשלה, הרשויות המקומיות ובמפקדות צבאיות.</p>
    <a id="site-link" href="https://inri.orc.org.il/">קישור</a>
    <p class="simple-text">בואו לעשות לנו לייק ולעקוב אחרינו ברשתות החברתיות, אתם גם ככה שם :)     </p>


    <span class="brands">
    <a href="https://www.facebook.com/ilResilience" target="_blank"><img class="brand" :src="faceBook" >
    </a>
    <a href="https://x.com/ILresilience" target="_blank"><img class="brand" :src="twitter" >
    </a>
    <a href="https://www.instagram.com/ilresilience/" target="_blank"><img class="brand" :src="instagram" >
    </a>
    <a href="https://www.instagram.com/ilresilience/" target="_blank"><img class="brand" :src="linkedin" >
    </a>
  </span>
    <p class="green-text">מידע על הכשרות צבאיות, נתונים היסטוריים ותוכן מקצועי</p>
    <p class="simple-text">עבור המידע הצבאי, מרחב המכללה מכיל XXX ויכול לעזור בכל מקרה שלZZZ. 
ניתן להיכנס דרך XX באמצעות חיפוש בXX</p>
<img class="image-content" :src="neve">
<p class="orange-text">יש לנו אפילו רשות מקומית דיגיטלית!</p>
    <p  class="simple-text">הכירו את נווה איתנים - הרשות הכי מוכנה במדינה :) 
בתוך מערכות השליטה והבקרה הזמינות לבעלי תפקידים בשעת חירום, הקמנו רשות מקוונת שניתן להתאמן עליה במגוון תרחישים. 
</p>
    <img :src="nextBtn" id="next-btn" @click="goToGif" >
  </div>
  <SocityNext v-if="state.showGif" @go-menu="backToMenu"></SocityNext>

  </div>
  </template>

<script setup>
import { reactive, onMounted, getCurrentInstance ,defineEmits, ref} from 'vue';
import nextBtn from "../assets/imgs/nextBtn.png";
import faceBook from "../assets/imgs/facebook.png";
import twitter from "../assets/imgs/twitter.png";
import instagram from "../assets/imgs/instagram.png";
import linkedin from "../assets/imgs/linkedin.png";
import comp from "../assets/imgs/collage-comp.png";
import neve from "../assets/imgs/neve.png";
import SocityNext from './SocityNext.vue';

const emit = defineEmits(['go-menu']);

const state = reactive({ 
showGif:false
});

const openFacebook = () => {
window.open("https://www.facebook.com/ilResilience", "_blank");
};


const goToGif = () =>{
  state.showGif=true;
  
}

const backToMenu = () =>{
    emit('go-menu');
}

const text1 = ref(null);
const text2 = ref(null);

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
font-size: 2.8em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "karantina";
color: rgb(89,89,89);
text-align: right;
}

.simple-text {
width: 100%;
height: auto;
margin-bottom: 2vh;
font-family: "Heebo";
font-size: 1.2em;
text-align: right;


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
.green-text {
font-size: 1.4em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color:rgb(59, 180, 140);
width: 95vw;
}
.orange-text {
font-size: 1.4em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color:rgb(255,140,0);
width: 95vw;
}
.grey-bold {
font-size: 1.2em;
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
.brand{
  height:auto;
  width:15vw
}
#site-link{
  font-size:1.3em; ;
  font-family: "Heebo";
  color:rgb(28, 180, 227);
  text-decoration: underline; /* Add underline */
}


</style>