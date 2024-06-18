<template>
  <div id="page">
      <div>
          <div id="scroll-text">
              <p ref="text1" class="grey-bold-text">כך נוצר מעגל ההכשרה השלם, המאפשר לנו לפגוש בבית אחד כמה שיותר בעלי תפקידים המנהלים מצבי חירום בתחומם</p>
              <!-- <img id="collageGif" src="../assets/imgs/collageGif.gif" alt="Collage Image">  להוסיף כאן גיף-->
              <div id="gif" ref="image1">מופיע כאן גיף</div>
              <p ref="text2"class="simple-text-big">בראשות המכללה ניצבת מפקדת בדרגת אל"ם ולרשותה מטה מקצועי המורכב ממשרתי קבע, מילואים ויועצים. סגל המרצים כולל מומחים מקצועיים מפיקוד העורף, רח"ל, משרדי הממשלה, המינהל הציבורי והאקדמיה.
              </p>
              <img class="image-content" :src="infoCollage1">
              <p class="simple-text">אנחנו גם מכשירים צוותי סע"ר (סיוע עצמי ראשוני) של הרשות המקומית ותלמידי כיתות י' לחילוץ קל - בכדי שיוכלו לסייע באירוע חילוץ בסביבה שלהם, כמו במקרה של רעידת אדמה. </p>
              <img class="image-content" :src="firefighters">
              <p class="simple-text">כיתות נבחרות מכל בתי הספר עוברות הכשרה של יומיים, בעוד צוותי הסע"ר לאחר ההכשרה, עוברים אימונים באתרי הרס בשיתוף ארגוני החירום הנוספים של הרשות. </p> 
                <p class="blue-text">מעניין, לא?</p>
                <p class="simple-text">את כל זה יש לנו גם בסרטון קצר ומגניב, אז בואו נראה קצת מספרים.
                       כדאי לנסות לזכור כמה שיותר פרטים, כי באיזשהו שלב תגיע שאלה..</p>
              <video id="video" src="../assets/media/videoCollage.mp4" controls ></video>
              <p class="grey-bold">בראשות המכללה ניצבת מפקדת בדרגת אל"ם ולרשותה מטה מקצועי המורכב ממשרתי קבע, מילואים ויועצים. סגל המרצים כולל מומחים מקצועיים מפיקוד העורף, רח"ל, משרדי הממשלה, המינהל הציבורי והאקדמיה.</p>
              <img  :src="nextBtn" id="next-wBtn2" @click="goToMenu">

      </div>
      </div>
  </div>
</template>


<script setup>
import { reactive, onMounted, getCurrentInstance ,defineEmits, ref} from 'vue';
import orange from "../assets/imgs/orange.png";
import collageGif from '../assets/imgs/collageGif.gif';
import nextBtn from "../assets/imgs/nextBtn.png";
import infoCollage1 from "../assets/imgs/infoCollage1.jpg";
import firefighters from "../assets/imgs/firefighters.jpg";
const emit = defineEmits(['go-menu']);


const goToMenu = () =>{
emit('go-menu');
}

const text1 = ref(null);
const text2 = ref(null);
const image1 = ref(null);
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
height: 250vh;
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
font-family: var(--font-family-karantina);
color: rgb(89,89,89);
}

.simple-text {
width: 100%;
height: auto;
margin-bottom: 2vh;
font-family: "Heebo";
font-size: 1.2em;

}
.simple-text-big {
width: 100%;
height: auto;
margin-bottom: 2vh;
font-family: "Heebo";
font-size: 1.4em;

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
font-family:"Heebo-Black";
color: rgb(89,89,89);
}

.grey-bold-text{
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

#next-btn{
position: absolute;
top:70vh;
right: 50%;
transform: translateX(50%);
animation: bounce 2s ease infinite; 

}

@keyframes bounce {
  0% {
      top: 70vh; /* Adjusted initial position */
  }
  50%{
    top: 75vh; /* Adjusted midpoint position */
  }
  100%{
    top: 70vh; /* Adjusted final position */
  }
}



#gif{
  display: block;
  width:90vw;
  height:20vh;
  background-color: aliceblue;

}

#video{
width:90vw;
height: auto;
}
.image-content {
width: 100%;
height: auto;
margin-bottom: 2vh;
}

#next-wBtn2{
position:absolute;
z-index: 5;
right:50%;
transform: translateX(50%);
top:40vh; /* Adjusted position */
animation: bounce2 2s ease infinite; 
}

@keyframes bounce2 {
  0% {
      top: 225vh; /* Adjusted initial position */
  }
  50%{
    top:220vh; /* Adjusted midpoint position */
  }
  100%{
    top: 225vh; /* Adjusted final position */
  }
}

</style>