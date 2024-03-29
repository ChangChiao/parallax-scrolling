<script setup>
import gsap from "gsap";
import JoinBtn from "./common/JoinBtn.vue";
import ScrollTrigger from "gsap/ScrollTrigger";
import { useMedia } from "../hooks/useMedia";
import { onMounted } from "vue";
const isMobile = useMedia();
gsap.registerPlugin(ScrollTrigger);
onMounted(() => {
  if (isMobile.value) {
    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: ".section-stage",
        pin: false,
        scrub: true,
        start: "top bottom",
        end: "bottom bottom",
      },
    });

    tl.fromTo(
      ".title-stage",
      { yPercent: -100 },
      {
        yPercent: 0,
        opacity: 1,
        direction: 1,
      }
    )
      .fromTo(
        ".stage-item-1",
        { yPercent: 100 },
        {
          yPercent: 0,
          opacity: 1,
          duration: 2,
        }
      )
      .fromTo(
        ".stage-item-2",
        { yPercent: 100 },
        {
          yPercent: 0,
          opacity: 1,
          duration: 2,
        }
      )
      .fromTo(
        ".stage-item-3",
        { yPercent: 100 },
        {
          yPercent: 0,
          opacity: 1,
          duration: 2,
        }
      );
    return;
  }

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: ".section-stage",
      pin: true,
      scrub: true,
      pinSpacing: false,
    },
  });

  // tl.fromTo(
  //   ".title-stage",
  //   { opacity: 0 },
  //   {
  //     opacity: 1,
  //     duration: 2,
  //   }
  // )
  tl.fromTo(".line-mask", { width: "100%" }, { width: 0, duration: 4 })
    .to(".stage-item-1", {
      opacity: 1,
      duration: 1,
    })
    .fromTo(
      ".stage-line-1",
      {
        scaleY: 0,
      },
      {
        opacity: 1,
        scaleY: 1,
      },
      "<"
    )
    .fromTo(
      ".stage-item-content-1",
      {
        opacity: 0,
        yPercent: 100,
      },
      {
        yPercent: 0,
        opacity: 1,
        duration: 2,
      },
      "-=2"
    )
    .to(".stage-item-2", {
      opacity: 1,
      duration: 1,
    })
    .fromTo(
      ".stage-line-2",
      {
        scaleY: 0,
      },
      {
        opacity: 1,
        scaleY: 1,
      },
      "<"
    )
    .fromTo(
      ".stage-item-content-2",
      {
        opacity: 0,
        yPercent: 100,
      },
      {
        yPercent: 0,
        opacity: 1,
        duration: 2,
      },
      "-=2"
    )
    .to(".stage-item-3", {
      opacity: 1,
      duration: 1,
    })
    .fromTo(
      ".stage-line-3",
      {
        scaleY: 0,
      },
      {
        opacity: 1,
        scaleY: 1,
      },
      "<"
    )
    .fromTo(
      ".stage-item-content-3",
      {
        opacity: 0,
        yPercent: 100,
      },
      {
        yPercent: 0,
        opacity: 1,
        duration: 2,
      },
      "-=2"
    )
    .set({}, {}, "+=6")
    .to(".section-stage", {
      opacity: 0,
    });
});
</script>

<template>
  <section class="pt-4 section section-stage">
    <h2 class="static opacity-0 title title-stage lg:absolute">重要時程</h2>
    <div
      class="flex flex-col items-center justify-between w-3/4 mx-auto stage-group lg:flex-row"
    >
      <div class="stage-item stage-item-1 lg:translate-y-[54px]">
        <div class="stage-item-content stage-item-content-1">
          <JoinBtn :isShowHand="true" />
          <h4 class="slogan">SIGN UP</h4>
          <span class="date">10/1 - 11/16</span>
          <p class="sub-title">截止前可修改報名組別</p>
        </div>
        <img
          class="w-6 for-mobile stage-line-1"
          src="../assets/main/date_weekLine.png"
          alt=""
        />
      </div>
      <div class="stage-item stage-item-2 lg:translate-y-[22px]">
        <div class="stage-item-content stage-item-content-2">
          <img class="w-24" src="../assets/main/date_start.png" alt="" />
          <h4 class="slogan">START</h4>
          <span class="date">10/31 - 11/28</span>
          <p class="sub-title">10/31(一) UI</p>
          <p class="sub-title">團體組開賽 11/7(一) 前端組開賽</p>
        </div>
        <img
          class="w-6 for-mobile stage-line-2"
          src="../assets/main/date_weekLine.png"
          alt=""
        />
      </div>
      <div class="stage-item stage-item-3 lg:translate-y-[50px]">
        <div class="stage-item-content stage-item-content-3">
          <img class="w-24" src="../assets/main/date_upload.png" alt="" />
          <h4 class="slogan">UPLOAD</h4>
          <span class="date">10/31 - 11/28</span>
          <p class="sub-title">依賽程登錄作品</p>
          <p class="remark">額外競賽： 主題豐厚獎金等著你</p>
        </div>
        <img
          class="w-6 for-mobile stage-line-3"
          src="../assets/main/date_weekLine.png"
          alt=""
        />
      </div>
    </div>
    <div class="relative for-mobile -scale-x-100">
      <img src="../assets/main/date_line.png" alt="" />
      <div class="absolute top-0 h-40 line-mask bg-secondary-normal"></div>
    </div>
  </section>
</template>
<style scoped>
.slogan {
  @apply pt-2 pb-2 text-center text-3xl tracking-wider  text-highlight-normal lg:text-6xl;
}
.date {
  @apply mb-2 rounded-3xl bg-primary-normal px-4 py-2 text-center text-xl text-white lg:text-4xl;
}
.stage-item {
  @apply mx-auto flex w-3/4 flex-col items-center py-10 opacity-0 lg:w-1/3 lg:pb-0;
  &-content {
    @apply flex flex-col items-center bg-secondary-normal;
  }
}

.for-mobile {
  @apply hidden lg:block;
}
</style>
