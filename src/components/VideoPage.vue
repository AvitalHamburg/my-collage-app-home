<template>
  <div id="page">
    <div id="scroll-text" v-if="!state.showSubj">
    <img class="image-content" :src="infoCollage1">
    <p class="simple-text">אנחנו גם מכשירים צוותי סע"ר (סיוע עצמי ראשוני) של הרשות המקומית ותלמידי כיתות י' לחילוץ קל - בכדי שיוכלו לסייע באירוע חילוץ בסביבה שלהם, כמו במקרה של רעידת אדמה. </p>
    <img class="image-content" :src="firefighters">
    <p class="simple-text">כיתות נבחרות מכל בתי הספר עוברות הכשרה של יומיים, בעוד צוותי הסע"ר לאחר ההכשרה, עוברים אימונים באתרי הרס בשיתוף ארגוני החירום הנוספים של הרשות. </p> 
      <p class="blue-text">מעניין, לא?</p>
      <p class="simple-text">את כל זה יש לנו גם בסרטון קצר ומגניב, אז בואו נראה קצת מספרים.
כדאי לנסות לזכור כמה שיותר פרטים, כי באיזשהו שלב תגיע שאלה..</p>
    <video id="video" src="../assets/media/videoCollage.mp4" controls ></video>

    <img :src="nextBtn" id="next-wBtn" @click.once="nextSubject">
    </div>
    <div id="scroll-text2" v-if="state.showSubj"> 
      <p class="grey-big">בראשות המכללה ניצבת מפקדת בדרגת אל"ם ולרשותה מטה מקצועי המורכב ממשרתי קבע, מילואים ויועצים. סגל המרצים כולל מומחים מקצועיים מפיקוד העורף, רח"ל, משרדי הממשלה, המינהל הציבורי והאקדמיה.</p>
      <img  :src="nextBtn" id="next-wBtn2" @click="goToMenu">
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, reactive } from 'vue';
import nextBtn from "../assets/imgs/nextBtn.png";
import infoCollage1 from "../assets/imgs/infoCollage1.jpg";
import firefighters from "../assets/imgs/firefighters.jpg";
const emit = defineEmits(['backMenu']);


const state = reactive({ 
  showSubj: false,
});


const nextSubject = () => {
  state.showSubj=true;
};
const goToMenu = () =>{
  console.log('backMenu in the video component');
  emit('backMenu');

};
</script>
<style scoped>

* {
overflow: hidden;
direction: rtl;
}
@font-face { 
  font-family: "Heebo-Black";
  font-weight: normal;
  src: url("../assets/fonts/Heebo-Black.woff"), 
       format("woff");
}

#page {
position: absolute;
top: 0%;
right: 50%;
transform: translateX(50%);
height: 100vh;
width: 100vw;
background-image: url("../assets/imgs/Bg2.png");
background-size: cover;
background-repeat: no-repeat;
padding: 0%;
}
#scroll-text {
/* Adjust positioning and dimensions */
position: absolute;
top: 16%;
left: 50%;
transform: translateX(-50%);
width: 90vw;
direction: rtl;
height:160vh ;

}
#scroll-text2 {
/* Adjust positioning and dimensions */
position: absolute;
top: 16%;
left: 50%;
transform: translateX(-50%);
width: 90vw;
direction: rtl;
height:100vh ;

}

#page-header{
  position: absolute;
  top:7vh;
  right: 50%;
  transform: translateX(50%);
  font-size: 2em;
  width: 90vw;
  text-overflow: none;
  color:rgb(31,56,100);
  font-family: "Heebo";
  text-align: center;
 
}

#user-massage{
  position: absolute;
  color:rgb(31,56,100);
  font-size: 1.5em;
  width:80vw;
  right:50%;
  transform: translateX(50%);
  bottom:25vh;
  font-family: "Heebo";
  text-align: center;
}

#video{
width:90vw;
height: auto;
}
@keyframes bounce2 {
  0% {
      top: 140vh; /* Adjusted initial position */
  }
  50%{
    top: 145vh; /* Adjusted midpoint position */
  }
  100%{
    top: 140vh; /* Adjusted final position */
  }
}

#next-wBtn{
position:absolute;
z-index: 5;
right:50%;
transform: translateX(50%);
bottom:-10vh; /* Adjusted position */
animation: bounce2 2s ease infinite; 
}
#next-wBtn2{
position:absolute;
z-index: 5;
right:50%;
transform: translateX(50%);
top:40vh; /* Adjusted position */
animation: bounce 2s ease infinite; 
}

@keyframes bounce {
  0% {
      top: 40vh; /* Adjusted initial position */
  }
  50%{
    top: 45vh; /* Adjusted midpoint position */
  }
  100%{
    top: 40vh; /* Adjusted final position */
  }
}
.image-content {
width: 100%;
height: auto;
margin-bottom: 2vh;
}

.titles-gray {
font-size: 2.5em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Karantina";
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
text-align: right;
}
.grey-bold {
font-size: 1.3em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color: rgb(89,89,89);
text-align: right;

}
.grey-big {
font-size: 1.5em;
margin-bottom: 2vh;
direction: rtl;
text-align: right;
font-family: "Heebo-Black";
color: rgb(89,89,89);
text-align: right;

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