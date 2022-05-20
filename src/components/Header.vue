<template>
<transition name="slidetop" appear>
  <div class="app-bar-wrapper">
    <div class="app-bar">
      <div class="app-bar-left">
        <img class="sev-logo" src="../assets/logo_white.png" />
        <div style="padding-left: 50px">
          <button class="button-container">
            <div class="flat-button-holder">Popular</div>
          </button>
        </div>
      </div>
      <div class="app-bar-right">
        <div class="main-navigation">
          <div class="nav-indicator"></div>
          <span class="nav-elem">Series</span>
          <span class="nav-elem">Movies</span>
          <span class="nav-elem">Serials</span>
          <span class="nav-elem">Sports</span>
          <span class="nav-elem">Kids</span>
        </div>
        <div class="nav-actions">
          <button class="button-container">
            <div class="icon-button-holder">
              <i
                class="far fa-search"
                style="color: white; font-size: 22px"
              ></i>
            </div>
          </button>
          <div style="width: 30px"></div>
          <button class="button-container">
            <div class="icon-button-holder">
              <i class="far fa-user" style="color: white; font-size: 22px"></i>
            </div>
          </button>
        </div>
      </div>
    </div>
  </div>
</transition>
</template>

<style scoped>
.app-bar-wrapper {
  position: relative;
  height: 100px;
  width: 100%;
  display: flex;
  justify-content: center;
}

.app-bar {
  height: 100%;
  width: 94%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.app-bar-left {
  height: 100%;
  display: flex;
  align-items: center;
}

.app-bar-right {
  display: flex;
  height: 100%;
}

.sev-logo {
  height: 100%;
}

.main-navigation {
  display: flex;
  position: relative;
  height: 100%;
  align-items: center;
  font-size: 18px;
  font-weight: 500;
}

.nav-elem {
  margin-right: 50px;
  cursor: pointer;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: rgba(255, 255, 255, 0.8);
  transition: all 0.2s, transform 0.25s;
}

.nav-elem:hover {
  color: rgba(255, 255, 255, 1);
  /* transform: scale(1.05); */
}

.nav-indicator {
  position: absolute;
  width: 40px;
  height: 2px;
  background-color: white;
  bottom: 26px;
  left: 0;
  pointer-events: none;
}

.nav-actions {
  position: relative;
  height: 100%;
  display: flex;
  align-items: center;
  padding-left: 40px;
}
</style>