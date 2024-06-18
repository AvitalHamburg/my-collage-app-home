<template>
    <div id="page">
        <div id="map"></div>
        <div v-for="i in indexs" :key="`orange${i}`" :id="'orange' + i" class="orange">
            <div v-for="j in indexs" :key="`white${j}`" :id="'white' + j" class="white"></div>
        </div>
    </div>
</template>

<script setup>
const indexs=[1,2,3,4,5]
</script>

<style scoped>
@font-face { 
  font-family: "Heebo";
  font-weight: normal;
  src: url("../assets/fonts/Heebo-VariableFont_wght.woff"), 
       format("woff");
}

#map {
    background-image: url("../assets/imgs/collageMap.png");
    width: 90vw;
    height: 60vh;
    background-size: cover;
    position: absolute;
    top: 10%;
    left: 50%; /* Added left property */
    transform: translateX(-50%); /* Adjusted transform to center horizontally */
    z-index: 0;
}
.orange {
    background-color: orange; /* צבע רקע כתום */
    border-radius: 50%; /* עיגול */
    width: 100px; /* רוחב */
    height: 100px; /* גובה */
    margin: 5px; /* מרווח בין העיגולים */
    display: inline-block; /* הצגה כבלוקים */
}
.white {
    background-color: white; /* צבע רקע לבן */
    border-radius: 50%; /* עיגול */
    width: 90px; /* רוחב */
    height: 90px; /* גובה */
    margin: 5px; /* מרווח בין העיגולים */
    display: inline-block; /* הצגה כבלוקים */
}
</style>
