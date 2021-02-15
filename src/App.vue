<template>
  <div>
    <link
      href="https://fonts.googleapis.com/css?family=Roboto&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="https://pro.fontawesome.com/releases/v5.15.2/css/all.css"
    />
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style>
html {
  overflow: hidden;
}

* {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
}

.button-container {
  user-select: none;
  outline: none;
  appearance: none;
  background-color: transparent;
  cursor: pointer;
}

.button-container.disabled {
  cursor: not-allowed;
}

.button-container.disabled .flat-icon-button-holder {
  background-color: rgba(66, 66, 66, 0.3);
  border: 1px solid rgba(66, 66, 66, 1) !important;
  color: rgba(66, 66, 66, 1);
}

.button-container.disabled .flat-icon-button-holder:hover {
}

.flat-button-holder {
  border-radius: 44px;
  border: 1px solid rgba(255, 255, 255, 0.6) !important;
  padding: 10px 36px;
  font-size: 0.9em;
  background-color: transparent;
  color: white;
  transition: all 0.2s;
  font-weight: 600;
  backdrop-filter: blur(30px);
}

.flat-button-holder:hover {
  background-color: white;
  color: black;
}

.icon-button-holder {
  width: 55px;
  height: 55px;
  background-color: transparent;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  backdrop-filter: blur(8px);
}

.flat-icon-button-holder {
  width: 55px;
  height: 55px;
  background-color: transparent;
  border: 1px solid #fff !important;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  font-size: 20px;
  color: white;
  backdrop-filter: blur(30px);
}

.flat-icon-button-holder:hover {
  background-color: rgba(255, 255, 255, 1);
  color: black;
}

.icon-button-holder:hover {
  background-color: rgba(255, 255, 255, 0.3);
}

.fadetop-enter-active,
.fadetop-leave-active {
  transition: opacity 0.8s ease-in-out,
    all 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}
.fadetop-enter-from,
.fadetop-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.slidetop-enter-active,
.slidetop-leave-active {
  transition: all 0.6s cubic-bezier(0, 0.55, 0.45, 1);
}
.slidetop-enter-from,
.slidetop-leave-to {
  transform: translateY(-100px);
}

.left-enter-active,
.left-leave-active {
  transition: all 0.6s ease;
}
.left-enter-from,
.left-leave-to {
  transform: translateX(-100%);
}

</style>

<style>
.lds-spinner {
  color: official;
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-spinner div {
  transform-origin: 40px 40px;
  animation: lds-spinner 1.2s linear infinite;
}
.lds-spinner div:after {
  content: " ";
  display: block;
  position: absolute;
  top: 3px;
  left: 37px;
  width: 6px;
  height: 18px;
  border-radius: 20%;
  background: #fff;
}
.lds-spinner div:nth-child(1) {
  transform: rotate(0deg);
  animation-delay: -1.1s;
}
.lds-spinner div:nth-child(2) {
  transform: rotate(30deg);
  animation-delay: -1s;
}
.lds-spinner div:nth-child(3) {
  transform: rotate(60deg);
  animation-delay: -0.9s;
}
.lds-spinner div:nth-child(4) {
  transform: rotate(90deg);
  animation-delay: -0.8s;
}
.lds-spinner div:nth-child(5) {
  transform: rotate(120deg);
  animation-delay: -0.7s;
}
.lds-spinner div:nth-child(6) {
  transform: rotate(150deg);
  animation-delay: -0.6s;
}
.lds-spinner div:nth-child(7) {
  transform: rotate(180deg);
  animation-delay: -0.5s;
}
.lds-spinner div:nth-child(8) {
  transform: rotate(210deg);
  animation-delay: -0.4s;
}
.lds-spinner div:nth-child(9) {
  transform: rotate(240deg);
  animation-delay: -0.3s;
}
.lds-spinner div:nth-child(10) {
  transform: rotate(270deg);
  animation-delay: -0.2s;
}
.lds-spinner div:nth-child(11) {
  transform: rotate(300deg);
  animation-delay: -0.1s;
}
.lds-spinner div:nth-child(12) {
  transform: rotate(330deg);
  animation-delay: 0s;
}
@keyframes lds-spinner {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
