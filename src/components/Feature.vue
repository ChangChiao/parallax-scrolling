<script setup>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import { useMedia } from "../hooks/useMedia";
import { onMounted, ref } from "vue";
const isMobile = useMedia();
gsap.registerPlugin(ScrollTrigger);
onMounted(() => {
  console.log("isMobile", isMobile.value);
  if (isMobile.value) {
    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: ".section-feature",
        pin: false,
        scrub: true,
        // markers: true,
        toggleClass: "active",
        start: "top center",
      },
    });
    tl.fromTo(
      ".title-feature",
      { yPercent: -100 },
      {
        yPercent: 0,
        opacity: 1,
        direction: 1,
      }
    )
      .fromTo(
        ".feature-1",
        { xPercent: -100 },
        {
          xPercent: 0,
          opacity: 1,
          duration: 1,
        }
      )
      .to(".feature-2", {
        opacity: 1,
        duration: 1,
        duration: 1,
      })
      .fromTo(
        ".feature-3",
        { xPercent: 100 },
        {
          xPercent: 0,
          opacity: 1,
          duration: 1,
        }
      )
      .set({}, {}, "+=4");
    return;
  }

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: ".section-feature",
      pin: true,
      scrub: true,
      // markers: true,
      pinSpacing: false,
      toggleClass: "active",
    },
  });
  tl.to(
    ".title-feature",
    {
      opacity: 1,
      duration: 1,
    },
    1
  )
    .to(
      ".grass-group",
      {
        scale: 1.25,
        opacity: 1,
      },
      "<"
    )
    .fromTo(
      ".feature-1",
      { xPercent: -100 },
      {
        opacity: 1,
        duration: 4,
        xPercent: 0,
      }
      // 2
    )
    .to(
      ".grass-group",
      {
        scale: 1,
        opacity: 1,
      },
      "<"
    )
    .to(
      ".feature-2",
      {
        opacity: 1,
        duration: 4,
      }
      // 5
    )
    .to(
      ".grass-group",
      {
        scale: 0.8,
        opacity: 0.8,
      },
      "<"
    )
    .fromTo(
      ".feature-3",
      { xPercent: 100 },
      {
        opacity: 1,
        duration: 4,
        xPercent: 0,
      }
      // 7
    )
    // .addPause(10)
    // .addLabel("blueGreenSpin", 4)
    .set({}, {}, "+=4")
    .to(
      ".grass-group",
      {
        scale: 0.5,
        opacity: 0.5,
      },
      "<"
    )
    .to(".section-feature", {
      opacity: 0,
      duration: 1,
    });
});
</script>

<template>
  <div class="section section-feature">
    <h2 class="title title-feature opacity-0">你是否也有以下困擾？</h2>
    <div class="wrapper items-center justify-between lg:flex lg:pt-10">
      <div class="feature feature-1">
        <h3 class="slogan">羨慕別人的酷酷網頁動畫？</h3>
        <img
          class="hidden lg:block"
          src="@/assets/main/question_1.png"
          alt=""
        />
        <img
          class="block lg:hidden"
          src="@/assets/main/question_1_m.png"
          alt=""
        />
      </div>
      <div class="feature feature-2">
        <h3 class="slogan">滿足不了同事的許願？</h3>
        <img class="" src="@/assets/main/question_2.png" alt="" />
      </div>
      <div class="feature feature-3">
        <h3 class="slogan">動畫技能樹太雜無從下手？</h3>
        <img
          class="hidden lg:block"
          src="@/assets/main/question_3.png"
          alt=""
        />
        <img
          class="block lg:hidden"
          src="@/assets/main/question_3_m.png"
          alt=""
        />
      </div>
    </div>
    <div
      class="grass-group fixed left-0 right-0 -bottom-4 mx-auto hidden w-2/3 origin-bottom scale-125 justify-between lg:flex"
    >
      <img class="w-1/6" src="@/assets/bg/bg_decorate_09.png" alt="" />
      <img class="w-1/6" src="@/assets/bg/bg_decorate_09.png" alt="" />
    </div>
  </div>
</template>
<style scoped>
.feature {
  @apply mx-auto w-[90%] opacity-0 lg:mr-3 lg:w-1/3;
}
.slogan {
  @apply pb-2 pt-10 text-center text-xl text-highlight-normal lg:pt-0 lg:text-4xl;
}
</style>
