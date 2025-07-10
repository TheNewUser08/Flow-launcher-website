<script setup>
import { ref } from "vue";
import { Menu, X } from "lucide-vue-next";

const isMenuOpen = ref(false);
</script>

<template>
  <nav
    class="fixed w-full md:w-3/4 text-lg left-1/2 transform -translate-x-1/2 top-0 p-4 bg-gray-900 text-gray-300 border-b md:border border-gray-700 shadow-lg md:rounded-lg z-200"
    style="
      background: linear-gradient(
        to top,
        rgba(17, 24, 39, 0.7) 70%,
        rgba(17, 24, 39, 0) 100%
      );
      backdrop-filter: blur(6px);
    "
  >
    <div class="flex items-center justify-between relative">
      <!-- Logo -->
      <div class="flex items-center">
        <img
          src="/FlowIcon.svg"
          alt="flow icon"
          class="h-5 w-5 inline-block mr-2"
        />
        <a href="/">Flow Launcher</a>
      </div>

      <!-- Desktop Menu -->
      <div class="hidden md:flex items-center gap-6">
        <a
          href="#plugins"
          class="text-gray-300 hover:text-white transition-colors"
          >Plugins</a
        >
        <a
          href="https://www.flowlauncher.com/docs/#/"
          class="text-gray-300 hover:text-white transition-colors"
          >Docs</a
        >
        <a href="https://www.flowlauncher.com/theme-builder">Theme Builder</a>
        <a
          href="https://github.com/Flow-Launcher/Flow.Launcher"
          target="_blank"
          rel="noopener"
          class="text-gray-300 hover:text-white transition-colors"
          >GitHub</a
        >
        <button
          class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 md:py-1 px-4 lg:px-6 rounded-lg min-w-[120px] transition-all hover:cursor-pointer border border-gray-700"
        >
          Download
        </button>
      </div>

      <!-- Mobile Menu Button -->
      <div class="md:hidden">
        <button @click="isMenuOpen = !isMenuOpen" class="text-white">
          <Menu v-if="!isMenuOpen" class="h-6 w-6" />
          <X v-else class="h-6 w-6" />
        </button>
      </div>
    </div>

    <!-- Mobile Menu Dropdown -->
    <div v-if="isMenuOpen" class="md:hidden mt-4">
      <ul class="flex flex-col items-center space-y-4">
        <li>
          <a
            href="#plugins"
            class="text-gray-300 hover:text-white transition-colors"
            >Plugins</a
          >
        </li>
        <li>
          <a
            href="https://www.flowlauncher.com/docs/#/"
            class="text-gray-300 hover:text-white transition-colors"
            >Docs</a
          >
        </li>
        <li>
          <a href="https://www.flowlauncher.com/theme-builder">Theme Builder</a>
        </li>
        <li>
          <a
            href="https://github.com/Flow-Launcher/Flow.Launcher"
            target="_blank"
            rel="noopener"
            class="text-gray-300 hover:text-white transition-colors"
            >GitHub</a
          >
        </li>
        <li>
          <button
            class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg w-full transition-all hover:cursor-pointer border border-gray-700"
          >
            Download
          </button>
        </li>
      </ul>
    </div>
  </nav>
</template>
