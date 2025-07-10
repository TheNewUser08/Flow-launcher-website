<script setup>
import NavBar from "./components/NavBar.vue";
// import FeatureCard from "./components/FeatureCard.vue";
import { motion, useScroll } from "motion-v";
const { scrollYProgress } = useScroll();
import { Search, Box, PenBox } from "lucide-vue-next";

import { ref } from "vue";
const sliderValue = ref(50);
</script>

<template class="bg-gray-900 m-5 z-10">
  <NavBar class="z-20" />
  <main class="flex flex-col items-center min-h-screen mt-50">
    <!-- SVG filter to create the grainy, blending texture -->
    <svg class="absolute w-0 h-0">
      <filter id="blending-noise">
        <feTurbulence
          type="fractalNoise"
          baseFrequency="0.7"
          numOctaves="1"
          stitchTiles="stitch"
          result="turbulence"
        />
        <feColorMatrix
          in="turbulence"
          type="saturate"
          values="0"
          result="noise"
        />
        <feComponentTransfer in="noise" result="noise">
          <feFuncR type="linear" slope="0.9" intercept="0.1" />
          <feFuncG type="linear" slope="0.5" intercept="0.2" />
          <feFuncB type="linear" slope="0.8" intercept="0.3" />
        </feComponentTransfer>
        <feColorMatrix
          in="noise"
          type="matrix"
          values="0 0 0 0 0 
                  0 0 0 0 0 
                  0 0 0 0 0 
                  0 0 0 -1 1"
          result="noiseMask"
        />
        <feComposite in="SourceGraphic" in2="noiseMask" operator="in" />
      </filter>
    </svg>

    <h1 class="relative isolate text-7xl font-bold text-center">
      <img
        src="/FlowIcon.svg"
        alt=""
        class="absolute w-2/5 left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 z-[-1] opacity-80"
        style="
          filter: url(#blending-noise);
          mask-image: radial-gradient(
              circle at center,
              black 30%,
              transparent 80%
            ),
            linear-gradient(to bottom, black 40%, transparent 100%);
          -webkit-mask-image: radial-gradient(
              circle at center,
              black 20%,
              transparent 80%
            ),
            linear-gradient(to bottom, black 40%, transparent 100%);
        "
      />
      <motion.div
        :initial="{ opacity: 0, transform: 'translateY(20px)' }"
        :animate="{ opacity: 1, transform: 'translateY(0px)' }"
        >The gateway to</motion.div
      >
      <motion.div
        :initial="{ opacity: 0, transform: 'translateY(20px)' }"
        :animate="{ opacity: 1, transform: 'translateY(0px)' }"
        :transition="{ delay: 0.5 }"
        >productivity</motion.div
      >
    </h1>
    <div class="flex flex-col space-y-2 items-center mt-10">
      <button
        class="flex p-2 bg-blue-600 opacity-90 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg min-w-[120px] transition-all hover:cursor-pointer border border-gray-700 shadow-lg"
      >
        <img src="/windows-11.png" alt="" class="w-6 mr-2" /> Download for
        Window
      </button>
      <span class="text-gray-500 text-sm">v1.20.1 - Jun 14, 2025</span>
    </div>
    <div class="flex flex-row items-center mt-10">
      <div class="text-right mr-10">
        <div>
          <h1 class="font-bold text-2xl">Start Flow Launcher anytime,</h1>
          <h1 class="font-bold text-2xl">anywhere.</h1>
        </div>
        <h2 class="text-gray-300 mt-2">
          Use your customizable hotkey to trigger the search window immediately.
        </h2>
      </div>
      <div>
        <img
          src="/flow-launcher.gif"
          alt=""
          class="w-120 h-auto border border-blue-100 rounded-lg shadow-lg shadow-gray-600"
          loading="lazy"
        />
      </div>
    </div>
    <div>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mt-4">
        <FeatureCard
          title="Customizable"
          description="Easily customize your search experience with plugins and themes."
          alt="Customizable Icon"
          :icon="PenBox"
        />
        <FeatureCard
          title="Fast Search"
          description="Find files, folders, and applications quickly with our powerful search engine."
          :icon="Search"
          alt="Fast Search Icon"
        />
        <FeatureCard
          title="Open Source"
          description="Flow Launcher is open source, allowing you to contribute and improve the project."
          alt="Open Source Icon"
          :icon="Box"
        />
      </div>
    </div>
    <div class="w-screen">
      <div class="p-10">
        <h2 class="text-xl font-bold">Community-made plugins</h2>
        <h3 class="text-gray-300">
          Write your own plugins in C#, F#, Python, JavaScript, or TypeScript.
        </h3>

        <div
          class="flex flex-nowrap overflow-x-auto space-x-6 justify-left mt-6 gap-6"
        >
          <ExtensionCard
            name="Obsidian"
            preview="/ObsidianExtension.avif"
            icon="/Obsidian.svg"
            author="Flow Community"
            description="An example plugin to showcase the capabilities of Flow Launcher."
          />
          <ExtensionCard
            name="Steam"
            preview="/SteamPreview.avif"
            icon="/Steam.svg"
            author="Garulf"
          />
          <ExtensionCard
            name="Obsidian"
            preview="/ObsidianExtension.avif"
            icon="/Obsidian.svg"
            author="Flow Community"
            description="An example plugin to showcase the capabilities of Flow Launcher."
          />
          <ExtensionCard
            name="Steam"
            preview="/SteamPreview.avif"
            icon="/Steam.svg"
            author="Garulf"
          />
          <ExtensionCard
            name="Obsidian"
            preview="/ObsidianExtension.avif"
            icon="/Obsidian.svg"
            author="Flow Community"
            description="An example plugin to showcase the capabilities of Flow Launcher."
          />
          <ExtensionCard
            name="Steam"
            preview="/SteamPreview.avif"
            icon="/Steam.svg"
            author="Garulf"
          />
        </div>
      </div>
    </div>
    <div>
      <h2 class="text-2xl font-bold text-center mt-16 mb-4">Customizations</h2>

      <div class="relative w-[800px] mx-auto my-8 select-none group">
        <!-- Dark mode image (background) -->
        <img
          src="/Flow dark.png"
          alt="Flow Launcher Dark"
          class="absolute inset-0 w-full h-full object-cover rounded-lg"
          draggable="false"
        />
        <img
          src="/Flow dark.png"
          alt="Flow Launcher Dark"
          class="inset-0 w-full h-full object-cover rounded-lg opacity-0"
          draggable="false"
        />
        <!-- Light mode image (foreground, clipped) -->
        <img
          src="/Flow light.png"
          alt="Flow Launcher Light"
          class="absolute inset-0 w-full h-full object-cover rounded-lg"
          :style="{
            clipPath: `polygon(0 0, ${sliderValue}% 0, ${sliderValue}% 100%, 0 100%)`,
          }"
          draggable="false"
        />

        <!-- Invisible Slider Input -->
        <input
          type="range"
          min="0"
          max="100"
          v-model="sliderValue"
          class="slider-input absolute inset-0 w-full h-[calc(100%+20px)] opacity-0 z-20 cursor-ew-resize"
        />

        <!-- Divider line and Custom Handle -->
        <div
          class="absolute top-0 bottom-0 w-1 bg-white/50 pointer-events-none z-10"
          :style="{ left: `${sliderValue}%` }"
        >
          <!-- Glassy Handle -->
          <div
            class="absolute bottom-0 translate-y-1/2 -translate-x-1/2 w-10 h-10 rounded-full bg-white/20 backdrop-blur-sm border-2 border-white/30 flex items-center justify-center"
          ></div>
        </div>
      </div>
    </div>
    <h1 class="text-2xl mt-10 text-center">
      Flow Launcher is a <b>free</b> and <b>open-source</b> software <br />
    </h1>

    <button
      class="bg-blue-800 text-xl border border-blue-600 rounded-xl p-4 m-7"
    >
      Support this project.
    </button>
  </main>
</template>
