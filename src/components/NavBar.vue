<script setup></script>

<template>
  <nav
    class="fixed w-3/4 text-lg left-1/2 transform -translate-x-1/2 top-0 p-4 bg-gray-900 text-gray-300 border border-gray-700 shadow-lg rounded-lg z-200"
    style="
      background: linear-gradient(
        to top,
        rgba(17, 24, 39, 0.7) 70%,
        rgba(17, 24, 39, 0) 100%
      );
      backdrop-filter: blur(6px);
    "
  >
    <ul class="flex items-center justify-between relative">
      <li class="flex items-center">
        <img
          src="/FlowIcon.svg"
          alt="flow icon"
          class="h-5 w-5 inline-block mr-2"
        />
        <strong>Flow Launcher</strong>
      </li>
      <li>
        <div class="flex items-center gap-10">
          <a
            href="#plugins"
            class="text-gray-300 hover:text-white transition-colors"
            >Plugins</a
          >
          <a
            href="#docs"
            class="text-gray-300 hover:text-white transition-colors"
            >Docs</a
          >
          <a href="#Theme">Theme Builder</a>
          <a
            href="https://github.com/Flow-Launcher/Flow.Launcher"
            target="_blank"
            rel="noopener"
            class="text-gray-300 hover:text-white transition-colors"
            >GitHub</a
          >
        </div>
      </li>
      <li>
        <button
          class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg min-w-[120px] transition-all hover:cursor-pointer border border-blue-300"
        >
          Download
        </button>
      </li>
    </ul>
  </nav>
</template>
