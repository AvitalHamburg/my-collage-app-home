

<template>
  <div id="intro">
    <div id="shadow"></div>
    <img :src="state.imagesrc" alt="White Logo" id="white-logo" :class="{ 'move-to-center': state.isLogoChanged }">
    <div  v-if="state.showIntro">
      <h1 id="welcome-text">ברוך הבא או הבאה למשפחת המכללה</h1>


      <p id="introduction"> בחצי שעה הקרובה תכירו ותלמדו על המכללה הלאומית לאיתנות ישראלית, במה אנחנו מתמחים, את מי אנחנו מכשירים, מאמנים ואיך כל זה קשור לשלטון העות'מאני.
        וכן, בארור שיש בוחן בסוף :) 
בהצלחה!</p>

      <img src="../assets/imgs/nextWhiteBtn.png"  id="next-wBtn" @click="moveNextPage"> 
    </div>
  </div>
</template>

<script setup>
import { reactive, onMounted, getCurrentInstance } from 'vue'

import whiteLogoGif from "../assets/imgs/whiteLogo.gif";
import inriLogoSvg from "../assets/imgs/inri-logo-white2.svg";

const { emit } = getCurrentInstance();

// משתנה בוליאני המציין האם המשתמש כבר היה בעמוד זה
let visitedThisPage = false;

const state = reactive({
  imagesrc: whiteLogoGif,
  isLogoChanged: false,
  showIntro: false,
  visitedThisPage: visitedThisPage  // הוספת המשתנה בוליאני לסטייט
});

function changeImageSourceAfterTimeout() {
  setTimeout(() => {
    state.imagesrc = inriLogoSvg;
    state.isLogoChanged = true;
    state.showIntro = true;
    state.visitedThisPage = true; // מסמנים שהמשתמש ביקר בעמוד זה
  }, 4000);
}

function moveNextPage(){
  emit("move-next", state.visitedThisPage); // שליחת הערך של visitedThisPage עם אירוע "move-next"
}

onMounted(() => {
  changeImageSourceAfterTimeout();
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
  font-family: "Karantina";
  font-weight: normal;
  src: url("../assets/fonts/Karantina-Regular.woff"), 
  format("woff");
} 



*{
  overflow: hidden;
  direction: rtl;
}
#intro {
  position:absolute;
  top: 0%;
  right: 50%;
  transform: translateX(50%);
  height: 100vh;
  width: 100vw;
  background-image: url("../assets/imgs/Bg1.png");
  background-size: cover;
  background-repeat: no-repeat;
  padding: 0%;
}
#shadow {
  height: 100vh;
  width: 100vw;
  position: absolute;
  background-color: rgb(59, 59, 59);
  top: 0%;
  right: 50%;
  transform: translateX(50%);
  opacity: 0.5;
  z-index: 2;
}

#white-logo {
  position: absolute;
  width: 50vw;
  height: auto;
  z-index: 5;
  right: 50%;
  transform: translateX(50%);
  top: 5%;
}
#welcome-text{
    color: white;
    position:absolute;
    right: 50%;
    transform: translateX(50%);
    font-size: 4em;
    text-align: center;
    top:15vh;
    z-index: 5;
    width:90vw;
    font-family: "karantina";

}
#introduction{
  position:absolute;
  color: white;
  right:50%;
  transform:translateX(50%);
  width:80vw;
  height:auto;
  z-index: 5;
  font-size: 1.7em;
  bottom:20vh;
  font-family: "Heebo"
}
@keyframes bounce2 {
	0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
	40% {transform: translateY(-30px);}
	60% {transform: translateY(-15px);}
}


#next-wBtn{
  position:absolute;
  z-index: 5;
  right:50%;
  transform: translateX(50%);
  bottom:20vh;   
  animation: bounce2 2s ease infinite; 
}
@keyframes bounce2 {
    0% {
        bottom: 15vh;
    }
    50%{
      bottom: 10vh;
    }
    100%{
      bottom: 15vh;
    }
}
.read-the-docs {
  color: #888;
}

.move-to-center {
  position: absolute;
  width: 50vw;
  height: auto;
  z-index: 5;
  right: 50%;
  transform: translateX(50%);
  top: 5%;
}




</style>


