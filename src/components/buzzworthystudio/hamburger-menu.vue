<script setup lang="ts">
import gsap from "gsap";

const links = ["Directors", "About", "Press", "Contact"];

const tl = gsap.timeline({
  defaults: {
    stagger: 0.1,
    duration: 0.3,
    ease: "power2.inOut",
  },
});

function handleMouseEnter() {
  if (tl.reversed()) tl.restart();
  gsap.to("#menu-background", {
    top: 0,
    right: 0,
    width: "100%",
    height: "100%",
    duration: 1,
    ease: "power4.inOut",
    borderRadius: 0,
  });
  tl.to("#hamburger-vertical > div", {
    y: "100%",
  });
  tl.to(
    "#hamburger-horizontal > div",
    {
      x: "0%",
      autoAlpha: 1,
    },
    "-=0.3",
  );
  gsap.to("#plus-icon", {
    autoAlpha: 1,
    rotate: 90,
    duration: 0.5,
    ease: "power2.inOut",
    delay: 0.3,
  });
  gsap.to("#links > h2", {
    autoAlpha: 1,
    y: 0,
    stagger: 0.05,
    duration: 0.5,
    ease: "power2.out",
    delay: 0.6,
  });
}

function handleMouseLeave() {
  gsap.to("#menu-background", {
    top: 32,
    right: 48,
    width: 112,
    height: 96,
    duration: 1,
    ease: "power4.inOut",
    borderRadius: 4,
  });
  tl.reverse();
  gsap.to("#plus-icon", {
    autoAlpha: 0,
    rotate: 0,
    duration: 0.5,
    ease: "power2.inOut",
  });
  gsap.to("#links > h2", {
    autoAlpha: 0,
    y: 40,
    stagger: {
      each: 0.05,
      from: "end",
    },
    duration: 0.5,
    ease: "power2.inOut",
  });
}

function handleLinkMouseEnter(index: number) {
  if (index === 1) return;
  gsap.to("#plus-icon", {
    rotate: (index + 2) * 90,
    duration: 0.5,
    ease: "power2.inOut",
  });
  gsap.to(`#link-${index} .white-letters`, {
    scaleY: 0,
    y: -4,
    stagger: {
      each: 0.02,
      from: "end",
    },
    duration: 0.3,
    ease: "power4.inOut",
  });
  gsap.to(`#link-${index} .red-letters`, {
    scaleY: 1,
    y: "0%",
    stagger: {
      each: 0.02,
      from: "end",
    },
    duration: 0.3,
    ease: "power4.inOut",
  });
}

function handleLinkMouseLeave(index: number) {
  if (index === 1) return;
  gsap.to("#plus-icon", {
    rotate: 90,
    duration: 0.5,
    ease: "power2.inOut",
  });
  gsap.to(`#link-${index} .white-letters`, {
    scaleY: 1,
    y: "0%",
    stagger: {
      each: 0.02,
      from: "end",
    },
    duration: 0.3,
    ease: "power4.inOut",
  });
  gsap.to(`#link-${index} .red-letters`, {
    scaleY: 0,
    y: 4,
    stagger: {
      each: 0.02,
      from: "end",
    },
    duration: 0.3,
    ease: "power4.inOut",
  });
}
</script>

<template>
  <main class="bg-stone-950 min-h-screen">
    <div @mouseleave="handleMouseLeave">
      <div class="fixed top-0 right-0 max-w-[68rem] w-full min-h-screen">
        <div
          id="menu-background"
          class="absolute top-8 right-12 w-28 h-24 bg-stone-800 rounded"
        ></div>

        <div
          class="relative min-h-screen flex flex-col justify-between pl-28 pt-28 pb-20"
        >
          <img id="plus-icon" src="/images/plus.svg" class="w-52 opacity-0" />

          <div id="links" class="flex flex-col items-start">
            <h2
              v-for="(link, index) in links"
              :id="`link-${index}`"
              class="text-[9rem] leading-[0.95] font-anton font-black uppercase opacity-0 translate-y-16 relative overflow-hidden"
              :class="
                index === 1 ? 'text-stone-700' : 'text-stone-50 cursor-pointer'
              "
              @mouseenter="handleLinkMouseEnter(index)"
              @mouseleave="handleLinkMouseLeave(index)"
            >
              <span
                class="inline-block origin-top white-letters"
                v-for="letter in link.split('')"
              >
                {{ letter }}
              </span>
              <div class="left-0 top-0 absolute">
                <span
                  class="inline-block origin-bottom text-red-500 scale-y-0 red-letters translate-y-1"
                  v-for="letter in link.split('')"
                >
                  {{ letter }}
                </span>
              </div>
            </h2>
          </div>
        </div>
      </div>

      <div
        class="fixed top-8 right-12 w-28 h-24 bg-stone-800 rounded flex justify-center items-center z-10"
        @mouseenter="handleMouseEnter"
      >
        <div class="relative overflow-hidden w-5 h-3.5 flex">
          <div
            id="hamburger-vertical"
            class="flex gap-0.5 absolute left-1/2 -translate-x-1/2 top-1/2 -translate-y-1/2"
          >
            <div class="w-0.5 h-3.5 bg-stone-50"></div>
            <div class="w-0.5 h-3.5 bg-stone-50"></div>
            <div class="w-0.5 h-3.5 bg-stone-50"></div>
          </div>
          <div
            id="hamburger-horizontal"
            class="flex flex-col gap-0.5 absolute left-1/2 -translate-x-1/2 top-1/2 -translate-y-1/2"
          >
            <div
              class="w-3.5 h-0.5 bg-stone-50 -translate-x-[125%] opacity-0"
            ></div>
            <div
              class="w-3.5 h-0.5 bg-stone-50 -translate-x-[125%] opacity-0"
            ></div>
            <div
              class="w-3.5 h-0.5 bg-stone-50 -translate-x-[125%] opacity-0"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
