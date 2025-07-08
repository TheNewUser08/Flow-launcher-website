<script setup>
import NavBar from "./components/NavBar.vue";
// import FeatureCard from "./components/FeatureCard.vue";
import { motion, useScroll } from "motion-v";
const { scrollYProgress } = useScroll();
import { Search, Box, PenBox } from "lucide-vue-next";
</script>

<template class="bg-gray-900">
  <NavBar class="z-20" />
  <main class="flex flex-col items-center min-h-screen mt-50 z-0">
    <h1 class="text-7xl font-bold text-center">
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
          class="w-120 h-auto border border-blue-100 rounded-lg"
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
        <div>
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
