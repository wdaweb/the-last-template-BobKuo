<template>
  <q-page class="flex flex-center" style="height: 1px">
    <swiper
      :style="{
        '--swiper-navigation-color': '#fff',
        '--swiper-pagination-color': '#fff',
      }"
      :speed="600"
      :slidesPerView="'auto'"
      :parallax="true"
      :freeMode="true"
      :mousewheel="true"
      :modules="modules"
      class="mySwiper"
      @slideChange="onSlideChange"
      @progress="onProgress"
      ref="swiperInstance"
    >
      <div
        slot="container-start"
        class="parallax-bg"
        :style="{
          'background-image':
            'url(https://rprojectjapan.com/assets/images/top/exhibition/bg_1_blur.webp)',
        }"
        data-swiper-parallax="-23%"
      ></div>
      <swiper-slide id="slide1">
        <h1 style="font-family: &quot;Kosugi Maru&quot;, sans-serif">
          歡迎光臨
        </h1>
        <h3 class="q-mt-none">Bob的最後模板作業</h3>
        <p>請用滑鼠滾輪移動頁面(swiper)</p>
        <p>滑鼠點入圖片會放大(gsap)</p>
        <p>開頭頁面的跳動使用animejs套件完成</p>
      </swiper-slide>
      <swiper-slide>
        <div class="card" @mouseenter="onCardHover" @mouseleave="onCardLeave">
          <img
            src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_1.webp"
          />
          <div ref="title1" class="title" data-swiper-parallax="100%">
            STORY
          </div>
          <div class="subtitle" data-swiper-parallax="-300">01</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card" @mouseenter="onCardHover" @mouseleave="onCardLeave">
          <img
            src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_2.webp"
          />
          <div ref="title2" class="title" data-swiper-parallax="0">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">02</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card" @mouseenter="onCardHover" @mouseleave="onCardLeave">
          <img
            src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_3.webp"
          />
          <div class="title" data-swiper-parallax="-200">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">03</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card" @mouseenter="onCardHover" @mouseleave="onCardLeave">
          <img
            src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_4.webp"
          />
          <div class="title" data-swiper-parallax="-300">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">04</div>
        </div>
      </swiper-slide>
    </swiper>
  </q-page>
</template>

<script setup>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";

import "swiper/css/pagination";
import "swiper/css/navigation";
import "swiper/css/free-mode";

// import required modules
import { Parallax, FreeMode, Mousewheel } from "swiper/modules";

// gsap
import { onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

// animejs
import { animate, stagger, text } from "animejs";

const modules = [Parallax, FreeMode, Mousewheel];

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  // 開頭
  const { chars } = text.split("#slide1 h1", { words: false, chars: true });

  if (chars && chars.length > 0) {
    animate(chars, {
      y: [
        { to: "-5rem", ease: "outExpo", duration: 1000 },
        { to: 0, ease: "outBounce", duration: 800, delay: 100 },
      ],
      rotate: {
        from: "-1turn",
        delay: 0,
      },
      delay: stagger(200),
      ease: "inOutCirc",
      loopDelay: 2000,
      loop: true,
    });
  }
});

const onCardHover = (event) => {
  const card = event.currentTarget;
  const img = card.querySelector("img");

  // 放大
  gsap.to(img, {
    scale: 1.2,
    duration: 0.5,
    ease: "power1.out",
  });
};

const onCardLeave = (event) => {
  const card = event.currentTarget;
  const img = card.querySelector("img");

  // 恢復圖片大小
  gsap.to(img, {
    scale: 1,
    duration: 0.5,
    ease: "power1.out",
  });
};
</script>

<style scoped>
#slide1 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.swiper {
  width: 100%;
  height: 100%;
  background: #000;
  /* border: 5px solid blue; */
}

.swiper-slide:nth-child(2n + 2) .card {
  /* border: 5px solid cyan; */

  position: absolute;
  top: 10%;
}
.swiper-slide:nth-child(2n + 3) .card {
  /* border: 5px solid magenta; */

  position: absolute;
  top: 20%;
}

.swiper-slide {
  width: 100%;

  font-size: 18px;
  color: #fff;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;

  .card {
    width: 85%;
    height: 50%;
  }

  img {
    width: 100%;
    height: 100%;

    position: absolute;
  }
  .title {
    font-family: "Archivo Black", sans-serif;

    font-size: 17px;
    font-weight: 1000;

    position: absolute;
    top: 60%;
    left: 0px;
  }
  .subtitle {
    font-family: "Archivo Black", sans-serif;
    font-size: 65px;

    position: absolute;
    top: 62%;
    left: 0%;
    text-decoration: underline;
  }
  .text {
    font-size: 14px;
    max-width: 400px;
    line-height: 1.3;
  }

  /* border: 1px solid green; */
}

.swiper-slide:nth-child(n + 2) {
  width: 50%;
}

.parallax-bg {
  position: absolute;
  left: 0;
  top: 0;
  width: 200%;
  height: 100%;
  -webkit-background-size: cover;
  background-size: cover;
  background-position: center;
}
</style>
