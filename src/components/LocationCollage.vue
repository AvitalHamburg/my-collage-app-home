<template>
  <div id="page">
   <div id="scroll-text">
    <p class="titles-gray" ref="text1"> מה נמצא איפה?
    </p>
    <p class="simple-text">רגע לפני סיום, קצת אוריינטציה בתוך בסיס הפיקוד, במשחק שצריך לתפוס ולגרור בו את שם המיקום לנקודות המתאימות במפה -</p>
   


    <img :src="nextBtn" id="next-btn" @click="backToMenu" >

  </div>
  </div>
  </template>

<script setup>
import { reactive, onMounted, getCurrentInstance ,defineEmits, ref} from 'vue';
import nextBtn from "../assets/imgs/nextBtn.png";
const emit = defineEmits(['go-menu']);


const backToMenu = () =>{
    emit('go-menu');
}

const text1 = ref(null);

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
#video{
width:90vw;
height: auto;
}

.button{
  background-color: rgb(28, 180, 227);
  border-radius: 50px;
  width:60vw;
  height:7vh;
  font-size: 1.5em;
  font-family: "Heebo-black";
}
#link{
  color:white
}

</style>