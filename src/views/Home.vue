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

      <Header></Header>
      
      <div class="main-container">
        <transition name="left" appear>
          <div
            class="dots-container"
            @click="
              episodes.push(episodes[0], episodes[1], episodes[2], episodes[3])
            "
          >
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
        </transition>
        <transition name="fadetop" appear>
          <div v-if="showP" class="middle-left">
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
              Elementum. Hic lorem ultrices. Eius, quasi dapibus suscipit ut
              massa litora sed, aliquet molestias, adipisci provident tenetur?
              Curae aut earum.Aenean repudiandae lacus. Mollitia ducimus
              ultricies qui tellus do, nisi tempus, voluptatibus sequi.
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
        </transition>
        <div style="width: 5%; height: 1px"></div>
        <div class="middle-right">
          <div
            class="right-top"
            ref="episodes_scroll"
            @wheel.prevent="episodesScroll"
            @scroll="setButtons"
          >
            <transition-group name="carousellist" appear>
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
            </transition-group>
            
            <div>
              <div ref="ep_scroll_spacer" style="height: 245px; display: flex; justify-content: center; align-items:center;">
                <div class="lds-spinner">
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
            </div>
              </div>
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
import Header from '../components/Header.vue';

export default {
  name: "Home",
  components: {
    Header,
  },
  data() {
    return {
      indicator: {
        leftBtn: "disabled",
        rightBtn: "",
      },
      showP: true,
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
        -40
          ? "disabled"
          : "";
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
  background-color: #000;
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

.carousellist-enter-active,
.carousellist-leave-active {
  transition: opacity 0.4s ease-in-out, all 0.8s cubic-bezier(0.64, 0, 0.78, 0);
}
.carousellist-enter-from,
.carousellist-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.carousellist-move {
  transition: all 0.3s ease;
}
</style>
