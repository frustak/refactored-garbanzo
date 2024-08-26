<script setup lang="ts">
import { PhArrowUpRight } from "@phosphor-icons/vue";
import gsap from "gsap";
import _ from "lodash";

const names = [
  "Calvin",
  "Douglass",
  "Janell",
  "Gail",
  "Eddie",
  "Trisha",
  "Beatrice",
  "Rhea",
  "Wilbur",
  "Phillip",
  "Willa",
];

const people = _.shuffle(
  names.map((name, index) => ({
    name,
    image: `/images/portraits/${index + 1}.jpg`,
  })),
);

function changeHeading(name: string) {
  gsap.to("#heading > span", {
    y: "-100%",
    stagger: {
      each: 0.02,
      from: "center",
    },
    duration: 0.3,
    ease: "power2.inOut",
  });
  gsap.to(`#name-${name.toLowerCase()} > span`, {
    y: "0%",
    stagger: {
      each: 0.02,
      from: "center",
    },
    duration: 0.3,
    ease: "power2.inOut",
  });
  gsap.to(`#name-${name.toLowerCase()} > span`, {
    y: "0%",
    stagger: {
      each: 0.02,
      from: "center",
    },
    duration: 0.3,
    ease: "power2.inOut",
  });
}

function resetHeading(name: string) {
  gsap.to("#heading > span", {
    y: "0%",
    stagger: {
      each: 0.02,
      from: "center",
    },
    duration: 0.3,
    ease: "power2.inOut",
  });
  gsap.to(`#name-${name.toLowerCase()} > span`, {
    y: "100%",
    stagger: {
      each: 0.02,
      from: "center",
    },
    duration: 0.3,
    ease: "power2.inOut",
  });
}

function moveCircleLink(event: MouseEvent) {
  const element = document.getElementById("circle-link");
  element?.animate([{ translate: `${event.clientX}px ${event.clientY}px` }], {
    duration: 500,
    fill: "forwards",
    easing: "ease-out",
  });
}
</script>

<template>
  <main
    class="flex flex-col items-center justify-center min-h-screen bg-stone-900 relative overflow-hidden"
    @mousemove="moveCircleLink"
  >
    <div class="flex items-center h-[10vw] justify-center">
      <div
        v-for="person in people"
        class="p-1 w-[5vw] cursor-pointer hover:w-[8vw] transition-all duration-300 group peer"
        @mouseenter="changeHeading(person.name)"
        @mouseleave="resetHeading(person.name)"
      >
        <img
          :src="person.image"
          class="object-cover transition duration-300 rounded-lg aspect-square grayscale group-hover:grayscale-0"
        />
      </div>

      <div
        id="circle-link"
        class="w-[9vw] h-[9vw] bg-red-500 rounded-full flex justify-center items-center text-white absolute top-0 left-0 scale-0 peer-hover:scale-100 transition duration-300 pointer-events-none z-10"
      >
        <PhArrowUpRight :size="24" weight="bold" />
      </div>
    </div>

    <div
      class="uppercase text-[16vw] font-black font-anton group overflow-hidden leading-tight relative text-center w-full"
    >
      <h1 id="heading" class="text-white">
        <span class="inline-block" v-for="letter in 'People'.split('')">
          {{ letter }}
        </span>
      </h1>
      <h2
        v-for="person in people"
        :id="`name-${person.name.toLowerCase()}`"
        class="text-red-500 absolute top-0 left-0 w-full"
      >
        <span
          class="inline-block translate-y-full"
          v-for="letter in person.name.split('')"
        >
          {{ letter }}
        </span>
      </h2>
    </div>
  </main>
</template>
