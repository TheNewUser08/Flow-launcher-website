<script setup>
import NavBar from "./components/NavBar.vue";
// import FeatureCard from "./components/FeatureCard.vue";
import { motion, useScroll, useSpring } from "motion-v";
const { scrollYProgress } = useScroll();
import { Search, Box, PenBox } from "lucide-vue-next";

import { ref, onMounted, onUnmounted } from "vue";
const sliderValue = ref(50);

const tabs = ref([
  { id: "developer", label: "Developer" },
  { id: "designer", label: "Designer" },
  { id: "note-taker", label: "Note Taker" },
]);
const activeTab = ref(tabs.value[0].id);

// --- Start of new code for drag-to-scroll ---
const extensionsContainer = ref(null);
const isDown = ref(false);
const startX = ref(0);
const scrollLeftStart = ref(0);

const onMouseDown = (e) => {
  e.preventDefault(); // Add this line
  isDown.value = true;
  if (extensionsContainer.value) {
    extensionsContainer.value.classList.add("active");
    startX.value = e.pageX - extensionsContainer.value.offsetLeft;
    scrollLeftStart.value = extensionsContainer.value.scrollLeft;
  }
};

const onMouseLeave = () => {
  isDown.value = false;
  if (extensionsContainer.value) {
    extensionsContainer.value.classList.remove("active");
  }
};

const onMouseUp = () => {
  isDown.value = false;
  if (extensionsContainer.value) {
    extensionsContainer.value.classList.remove("active");
  }
};

const onMouseMove = (e) => {
  if (!isDown.value || !extensionsContainer.value) return;
  e.preventDefault();
  const x = e.pageX - extensionsContainer.value.offsetLeft;
  const walk = (x - startX.value) * 2; // Multiplier for scroll speed
  extensionsContainer.value.scrollLeft = scrollLeftStart.value - walk;
};
// --- End of new code for drag-to-scroll ---
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
      <motion.button
        class="p-px text-white font-semibold rounded-3xl min-w-[120px] transition-all hover:cursor-pointer shadow-lg bg-gradient-to-b from-blue-400 to-transparent"
        :whileHover="{ backgroundColor: '#1f2937' }"
        :transition="{ duration: 0.1, type: 'spring', bounce: 0.3 }"
      >
        <div class="flex bg-gray-900 rounded-[18px] px-6 py-2">
          <img src="/windows-11.png" alt="" class="w-6 mr-2" /> Download for
          Window
        </div>
      </motion.button>

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

    <div class="w-full">
      <div>
        <div class="relative flex justify-center space-x-10 p-1">
          <button
            v-for="tab in tabs"
            :key="tab.id"
            @click="activeTab = tab.id"
            :class="[
              'relative rounded-full px-4 py-2 text-sm font-medium transition',
              activeTab === tab.id
                ? 'text-white'
                : 'text-gray-400 hover:text-white',
            ]"
            style="z-index: 10"
          >
            <motion.div
              v-if="activeTab === tab.id"
              class="absolute inset-0 p-px rounded-3xl bg-gradient-to-b from-blue-400 to-transparent"
              layoutId="active-pill-bg"
              :transition="{ duration: 0.6, type: 'spring', bounce: 0.3 }"
            >
              <motion.div class="bg-gray-900 rounded-[23px] p-4"> </motion.div>
            </motion.div>
            <span class="relative">{{ tab.label }}</span>
          </button>
        </div>
        <img src="/background desktop.png" alt="" />
      </div>
    </div>
    <div class="w-full max-w-screen-lg px-4">
      <div class="p-10">
        <h2 class="text-xl font-bold">Community-made plugins</h2>
        <h3 class="text-gray-300">
          Write your own plugins in C#, F#, Python, JavaScript, or TypeScript.
        </h3>

        <div
          ref="extensionsContainer"
          class="grid grid-flow-col auto-cols-max overflow-x-auto space-x-6 justify-left mt-6 gap-6 py-10"
          @mousedown="onMouseDown"
          @mouseleave="onMouseLeave"
          @mouseup="onMouseUp"
          @mousemove="onMouseMove"
        >
          <ExtensionCard
            name="Obsidian"
            preview="/ObsidianExtension.avif"
            icon="/Obsidian.svg"
            author="Flow Community"
            description="Search and open your Obsidian vaults, notes, and files."
          />
          <ExtensionCard
            name="Steam"
            preview="/SteamPreview.avif"
            icon="/Steam.svg"
            author="Garulf"
            description="Quickly launch your favorite Steam games."
          />
          <ExtensionCard
            name="Spotify"
            preview="/Spotify plugin.avif"
            icon="/spotify.svg"
            author="fow5040"
            description="Control your Spotify playback, search songs, and manage playlists."
          />

          <ExtensionCard
            name="Github"
            preview="/githubPreview.avif"
            icon="/github_dark.svg"
            author="Flow Community"
            description="Search for repositories, issues, and pull requests on GitHub."
          />

          <ExtensionCard
            name="Clipboard History"
            preview="/ClipboardHistoryPreview.png"
            icon="/clipboard.png"
            author="Jack251970"
            description="An example plugin to showcase the capabilities of Flow Launcher."
          />
          <div class="flex items-center justify-center">
            <a
              href="https://www.flowlauncher.com/plugins"
              class="text-white font-semibold bg-blue-600 opacity-90 hover:bg-blue-700 py-2 px-3 border text-sm border-blue-800 rounded-lg hover:shadow-lg text-center"
            >
              View all
            </a>
          </div>
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
