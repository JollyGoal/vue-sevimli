<template>
  <div style="position: relative">
    <div class="main-wrapper">
      <div style="position: absolute; left: 0; top: 0">
        <video
          class="main-video"
          autoplay
          muted
          loop
          src="https://test-videos.co.uk/vids/sintel/mp4/av1/1080/Sintel_1080_10s_1MB.mp4"
        ></video>
        <div class="main-video-wrapper"></div>
      </div>
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
                  <i
                    class="far fa-user"
                    style="color: white; font-size: 22px"
                  ></i>
                </div>
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="main-container">
        <div class="dots-container">
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
          <div class="dot-divider"></div>
          <div class="dot-indicator"></div>
        </div>
        <div class="middle-left">
          <div class="main-rating">
            <i class="fas fa-star main-rating-star"></i>
            <i class="fas fa-star main-rating-star"></i>
            <i class="fas fa-star main-rating-star"></i>
            <i class="fas fa-star-half-alt main-rating-star"></i>
            <i class="fal fa-star main-rating-star"></i>
            <div style="padding-left: 10px" class="main-description">
              7.9/10
            </div>
          </div>
          <div class="main-title">Winter Is Coming</div>
          <div class="main-description">
            Elementum. Hic lorem ultrices. Eius, quasi dapibus suscipit ut massa
            litora sed, aliquet molestias, adipisci provident tenetur? Curae aut
            earum.Aenean repudiandae lacus. Mollitia ducimus ultricies qui
            tellus do, nisi tempus, voluptatibus sequi.
          </div>
          <div class="main-play-area">
            <button class="button-container">
              <div class="flat-icon-button-holder">
                <i class="far fa-play" style="transform: translateX(2px)"></i>
              </div>
            </button>
            <div class="play-label">Watch Trailer</div>
          </div>
        </div>
        <div style="width: 5%; height: 1px"></div>
        <div class="middle-right">
          <div
            class="right-top"
            ref="episodes_scroll"
            @wheel.prevent="episodesScroll"
            @scroll="setButtons"
          >
            <div
              class="carousel-item"
              :class="index + 1 === active_episode_index ? 'active' : ''"
              v-for="(episode, index) in episodes"
              :key="index"
            >
              <img class="carousel-item-image" :src="episode.poster" />
              <div class="carousel-item-content">
                <div class="episode-meta">Episode {{ index + 1 }}</div>
                <div class="episode-title">{{ episode.title }}</div>
                <div class="episode-meta">
                  <i class="fas fa-star" style="padding-right: 8px"></i
                  >{{ episode.rating }}
                </div>
              </div>
            </div>
            <div>
              <div ref="ep_scroll_spacer" style="height: 245px"></div>
            </div>
          </div>
          <div class="right-bottom">
            <div style="display: flex">
              <button
                class="button-container"
                :class="indicator.leftBtn"
                @click="episodesScroll(-1)"
              >
                <div class="flat-icon-button-holder">
                  <i class="far fa-chevron-left" style=""></i>
                </div>
              </button>
              <div style="width: 16px"></div>
              <button
                class="button-container"
                :class="indicator.rightBtn"
                @click="episodesScroll(1)"
              >
                <div class="flat-icon-button-holder">
                  <i class="far fa-chevron-right" style=""></i>
                </div>
              </button>
            </div>
            <div
              style="
                display: flex;
                align-items: center;
                padding-right: 50px;
                font-weight: bold;
                letter-spacing: 2px;
              "
            >
              <div style="cursor: pointer" @click="episodesScroll('start')">
                01
              </div>
              <div
                style="
                  width: 35px;
                  height: 1px;
                  background-color: white;
                  margin: 0 20px;
                "
              ></div>
              <div style="cursor: pointer" @click="episodesScroll('end')">
                {{ ("0" + episodes.length).slice(-2) }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import Header from "../components/Header"

export default {
  name: "Home",
  components: {
    // Header,
  },
  data() {
    return {
      indicator: {
        leftBtn: "disabled",
        rightBtn: "",
      },
      recommendations: [{}],
      active_episode_index: 1,
      episodes: [
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/bw6DlqljVFIinhBA7uDSNha6Lnp.jpg",
          rating: "9,3",
        },
        {
          title: "Winter is coming",
          poster:
            "https://www.themoviedb.org/t/p/original/rlKI5ErcB5dhcvkpb8RAuDkBdhO.jpg",
          rating: "6,2",
        },
        {
          title: "White Dead",
          poster:
            "https://www.themoviedb.org/t/p/original/mc2dQBpxR1vJpOOqZVAqY9sQHOc.jpg",
          rating: "9,3",
        },
        {
          title: "Crown",
          poster:
            "https://www.themoviedb.org/t/p/original/fnpyUJ2Y2xk9mMQUrcRB4JNnCHT.jpg",
          rating: "9,3",
        },
        {
          title: "Throne",
          poster:
            "https://www.themoviedb.org/t/p/original/4KHspQhxzwKV52g1y8fNcqgtro1.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/5Hpk46yTgrnGB12fVATs1GUQfi.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/bw6DlqljVFIinhBA7uDSNha6Lnp.jpg",
          rating: "9,3",
        },
        {
          title: "Winter is coming",
          poster:
            "https://www.themoviedb.org/t/p/original/rlKI5ErcB5dhcvkpb8RAuDkBdhO.jpg",
          rating: "6,2",
        },
        {
          title: "White Dead",
          poster:
            "https://www.themoviedb.org/t/p/original/mc2dQBpxR1vJpOOqZVAqY9sQHOc.jpg",
          rating: "9,3",
        },
        {
          title: "Crown",
          poster:
            "https://www.themoviedb.org/t/p/original/fnpyUJ2Y2xk9mMQUrcRB4JNnCHT.jpg",
          rating: "9,3",
        },
        {
          title: "Throne",
          poster:
            "https://www.themoviedb.org/t/p/original/4KHspQhxzwKV52g1y8fNcqgtro1.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/5Hpk46yTgrnGB12fVATs1GUQfi.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/bw6DlqljVFIinhBA7uDSNha6Lnp.jpg",
          rating: "9,3",
        },
        {
          title: "Winter is coming",
          poster:
            "https://www.themoviedb.org/t/p/original/rlKI5ErcB5dhcvkpb8RAuDkBdhO.jpg",
          rating: "6,2",
        },
        {
          title: "White Dead",
          poster:
            "https://www.themoviedb.org/t/p/original/mc2dQBpxR1vJpOOqZVAqY9sQHOc.jpg",
          rating: "9,3",
        },
        {
          title: "Crown",
          poster:
            "https://www.themoviedb.org/t/p/original/fnpyUJ2Y2xk9mMQUrcRB4JNnCHT.jpg",
          rating: "9,3",
        },
        {
          title: "Throne",
          poster:
            "https://www.themoviedb.org/t/p/original/4KHspQhxzwKV52g1y8fNcqgtro1.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/5Hpk46yTgrnGB12fVATs1GUQfi.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/bw6DlqljVFIinhBA7uDSNha6Lnp.jpg",
          rating: "9,3",
        },
        {
          title: "Winter is coming",
          poster:
            "https://www.themoviedb.org/t/p/original/rlKI5ErcB5dhcvkpb8RAuDkBdhO.jpg",
          rating: "6,2",
        },
        {
          title: "White Dead",
          poster:
            "https://www.themoviedb.org/t/p/original/mc2dQBpxR1vJpOOqZVAqY9sQHOc.jpg",
          rating: "9,3",
        },
        {
          title: "Crown",
          poster:
            "https://www.themoviedb.org/t/p/original/fnpyUJ2Y2xk9mMQUrcRB4JNnCHT.jpg",
          rating: "9,3",
        },
        {
          title: "Throne",
          poster:
            "https://www.themoviedb.org/t/p/original/4KHspQhxzwKV52g1y8fNcqgtro1.jpg",
          rating: "9,3",
        },
        {
          title: "Dragon Stone",
          poster:
            "https://www.themoviedb.org/t/p/original/5Hpk46yTgrnGB12fVATs1GUQfi.jpg",
          rating: "9,3",
        },
      ],
    };
  },
  mounted: function () {
    // Add episodes carousel placeholder
    this.setCaruselEmpty();

  },
  watch: {},
  methods: {
    setCaruselEmpty() {
      this.newWidth = this.$refs.episodes_scroll.offsetWidth - 285;
      this.$refs.ep_scroll_spacer.style.width = this.newWidth.toString() + "px";
    },
    setButtons() {
      this.indicator.leftBtn =
        this.$refs.episodes_scroll.scrollLeft === 0 ? "disabled" : "";
      // this.indicator.rightBtn =
      this.indicator.rightBtn =
        this.$refs.episodes_scroll.scrollLeft +
          285 +
          this.$refs.ep_scroll_spacer.offsetWidth -
          this.$refs.episodes_scroll.scrollWidth >=
          -40 ? "disabled" : ""
    },
    episodesScroll(dir) {
      // console.log(dir);
      if (dir === "end") {
        this.handleAfterScroll(1000);
        this.$refs.episodes_scroll.scrollBy({
          left: this.$refs.episodes_scroll.scrollWidth,
        });
        return;
      } else if (dir === "start") {
        this.handleAfterScroll(1000);
        this.$refs.episodes_scroll.scrollBy({
          left: -this.$refs.episodes_scroll.scrollWidth,
        });
        return;
      }
      this.handleAfterScroll();

      if (dir.deltaY > 0 || dir.deltaX > 0) {
        this.$refs.episodes_scroll.scrollBy({ left: 280 });
        return;
      }

      if (dir.deltaY < 0 || dir.deltaX < 0) {
        this.$refs.episodes_scroll.scrollBy({ left: -280 });
        return;
      }

      // if (dir.deltaY !== 0 || dir.deltaXd !== 0) {
      //   this.$refs.episodes_scroll.scrollBy({ left: 280 });
      //   return
      // }

      // this.scroll = (this.$refs.episodes_scroll.offsetWidth / 1.5) * dir;
      this.scroll = 280 * dir;
      this.$refs.episodes_scroll.scrollBy({ left: this.scroll });
    },
    handleAfterScroll(timeout = 500) {
      if (this.episode_timer) clearTimeout(this.episode_timer);

      this.episode_timer = setTimeout(() => {
        this.index = Math.round(this.$refs.episodes_scroll.scrollLeft / 285);
        this.active_episode_index = this.index + 1;
      }, timeout);
    },
  },
};
</script>

<style scoped>
.main-wrapper {
  position: relative;
  width: 100vw;
  height: 100vh;
  background-color: #ecebec;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.main-video-wrapper {
  position: absolute;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  /* background: radial-gradient(transparent , rgba(0, 0, 0, 0.8)) rgba(0, 0, 0, 0.3); */
  background: rgba(0, 0, 0, 0.5);
}

.main-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
}

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
  color: rgba(255, 255, 255, 0.9);
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

.sev-logo {
  height: 100%;
}

.main-container {
  width: 98% !important;
  height: 100%;
  position: relative;
  width: 100%;
  display: flex;
}

.dots-container {
  width: 100px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.dot-divider {
  width: 1px;
  height: 80px;
  background-color: rgba(73, 73, 73, 0.8);
}

.dot-indicator {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background-color: rgba(73, 73, 73, 0.8);
}

.middle-left {
  position: relative;
  width: 45%;
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.main-rating {
  display: flex;
  align-items: center;
}

.main-rating-star {
  font-size: 1.4em;
  padding-right: 6px;
}

.main-title {
  letter-spacing: 1px;
  font-size: 64px;
  text-align: start;
  padding: 24px 0;
  font-weight: bold;
}

.main-description {
  text-align: start;
  font-size: 18px;
  color: rgba(255, 255, 255, 0.6);
  line-height: 2;
}

.main-play-area {
  display: flex;
  align-items: center;
  padding-top: 35px;
}

.play-label {
  letter-spacing: 1px;
  padding-left: 20px;
  font-weight: bold;
  font-size: 18px;
}

.middle-right {
  position: relative;
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.right-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 0;
}

.right-top {
  position: relative;
  width: 100%;
  height: 500px;
  display: flex;
  align-items: center;
  overflow-x: visible;
  overflow-y: hidden;
  scroll-behavior: smooth;
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
  scroll-snap-type: x proximity;
}

.right-top::-webkit-scrollbar {
  display: none;
  -webkit-appearance: none;
  width: 0;
  height: 0;
}

.carousel-item {
  position: relative;
  scroll-snap-align: start;
  border-radius: 14px;
  height: 350px;
  width: 245px;
  margin: 0 20px;
  cursor: pointer;
  transition: all 0.15s;
}

.carousel-item-image {
  position: relative;
  top: 0;
  left: 0;
  background-color: white;
  border-radius: 14px;
  object-fit: cover;
  height: 350px;
  width: 245px;
  pointer-events: none;
  transition: all 0.15s;
}

.carousel-item.active {
  /* transform: scale(1.05); */
  height: 400px;
  width: 280px;
}

.carousel-item.active .carousel-item-image {
  /* transform: scale(1.05); */
  height: 400px;
  width: 280px;
}

.right-top div:first-child {
  margin: 0 20px 0 0;
}

.carousel-item-content {
  position: absolute;
  bottom: 20px;
  left: 20px;
  display: flex;
  flex-direction: column;
}

.episode-meta {
  text-align: start;
}

.episode-title {
  text-align: start;
  font-weight: bold;
  font-size: 1.3em;
  padding: 10px 0 12px 0;
}
</style>
