<template>
  <div>
    <HelloWorld v-if="state.page === 0" @move-next="nextPage"></HelloWorld>
    
    <div :class="{ 'open': state.openHamburger }" id="hamburger-icon" v-if="state.page > 0" @click="showHamburger">
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
  </div>
    <div class="trancperncy"></div>
    <header id="header" v-if="state.page && !state.openHamburger">
    <img v-if="!state.openHamburger" :src="collegeLogo" id="logo" @click="backToMenu">
    <img v-if="!state.openHamburger && state.textNum !== 2 " id="shape" :src="orange">
    <img v-if="!state.openHamburger && state.textNum !== 2 "  id="shape1" :src="blue">
    <img v-if=" state.textNum === 2 " id="shape" :src="red">
    <img v-if=" state.textNum === 2 " id="shape1" :src="red">

   </header>

    <Menu v-if="state.showMenu" :visitedMenuPage="state.visitedPages" @go-next="movePage"></Menu>
    <KnowCollage v-if="state.textNum === 1" @go-menu="nextSubj"></KnowCollage>
    <ActiveCollage v-if="state.textNum === 2" @go-menu="nextSubj"></ActiveCollage>
    <SocityCollage v-if="state.textNum === 3" @go-menu="nextSubj"></SocityCollage>
    <LibraryCollage v-if="state.textNum === 4" @go-menu="nextSubj"></LibraryCollage>
    <OutsideCollage v-if="state.textNum === 5" @go-menu="nextSubj"></OutsideCollage>
    <LocationCollage v-if="state.textNum === 6"  @go-menu="nextSubj"></LocationCollage>
    <LocationCollage v-if="state.textNum === 6"  @go-menu="nextSubj"></LocationCollage>
    <Game v-if="state.textNum === 7"  @go-menu="backToMenu"></Game>

    <div class="overlay" v-if="state.openHamburger" @click="showHamburger">
    </div>
    <Hamburger 
      id="hamburger-page" 
      v-if="state.openHamburger" 
      :visitedMenuPage="state.visitedPages" 
      @next-page="movePage"
    ></Hamburger>  </div>
</template>

<script setup>
import { reactive } from 'vue';
import Menu from './components/Menu.vue';
import Game from './components/Game.vue';
import Hamburger from './components/Hamburger.vue';
import HelloWorld from './components/HelloWorld.vue';
import KnowCollage from './components/KnowCollage.vue';
import ActiveCollage from './components/ActiveCollage.vue';
import OutsideCollage from './components/OutsideCollage.vue';
import TrainingCollage from './components/SocityNext.vue';
import LocationCollage from './components/LocationCollage.vue';
import LibraryCollage from './components/LibraryCollage.vue';
import SocityCollage from './components/SocityCollage.vue';
import collegeLogo from "./assets/imgs/collegeLogo.png";
import orange from "./assets/imgs/orange.png";
import blue from "./assets/imgs/blue.png";
import red from "./assets/imgs/red.png";


const state = reactive({
  page: 0,
  showMenu: false,
  textNum: 0,
  openHamburger:false,
  visitedPages: []
});

function nextPage() {
  state.page++;
  state.showMenu = true;
}

const movePage = (number) => {
  state.textNum = number;
  state.showMenu = false;
  state.openHamburger=false;
  state.visitedPages.push(number-1);
}

const nextSubj = () => {
  state.textNum++;
}

const backToMenu = () =>{
      state.showMenu=true;
}

const showHamburger = () =>{
      state.openHamburger = !state.openHamburger;
}
</script>

<style scoped>
body {
  height: 100vh;
  width: 100vw;
  background-size: cover;
  background-repeat: no-repeat;
  overflow: hidden;
  position: relative;
  background-image: url("../assets/imgs/Bg2.png");
  padding: 0%;

}

.trancperncy{
  position: absolute;
  height: 8vh;
  top: 0;
  width: 100vw;
  right: 50%;
  transform: translateX(50%);
  z-index: 8899;
  opacity: 0.8;
}

header {
  position: absolute;
  height: 8vh;
  top: 0;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: space-between;
  right: 50%;
  transform: translateX(50%);
  z-index: 9999;
  background-color: aliceblue;

  /* background-image: url("./assets/imgs/header.png"); */
  background-size: cover;
}

@keyframes slideIn {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: #175a85; 
  box-shadow: 0 0 20px rgba(23, 90, 133, 0.2);  /* Adjust the transparency as needed */
  z-index: 8998; /* Make sure the overlay is below the hamburger menu but above other content */
  transition: transform 0.5s; 
  animation: slideIn 0.5s forwards; 
}
#hamburger-page {
  position: fixed;
  top: 10vh;
  right: 0;
  width: 100vw; 
  height: 100vh; 
  transition: transform 0.5s; 
  animation: slideIn 0.5s forwards; 
  margin-top: 10vh; /* Adjust the margin-top value as needed */
  z-index: 9999;
}


#hamburger-icon {
  position: absolute;
  top: 0.5vh; 
  left: 2vw; 
  width: 10vw;
  height: 10vh; 
  z-index: 19999; 
}

.bar {
  width: 8vw;
  height: 0.8vw;
  background-color: black;
  margin: 2vw 0;
  transition: 0.4s;
  border-radius: 500px;
}

#hamburger-icon.open .bar:nth-child(1) {
  transform: rotate(-45deg) translate(-1.6vw, 1vw);
  background-color: aliceblue;
}

#hamburger-icon.open .bar:nth-child(2) {
  opacity: 0;
}

#hamburger-icon.open .bar:nth-child(3) {
  transform: rotate(45deg) translate(-3vw, -2.6vw);
  background-color: aliceblue;
}
#logo{
  position: absolute;
  z-index: 9999; 
  height: 7vh;
  width: auto;
  right: 5%;
  top: 8%;
}
#shape{
  position: absolute;
  left:0%;
  top:0%;
  height: 20vh;
  z-index: 9997; 

}
#shape1{
  position: absolute;
  right: 0%;
  height: 13vh;
  bottom: -92vh; 
  transform: rotate(180deg);


}



</style>

