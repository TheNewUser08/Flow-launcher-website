<template>
  <div
    class="relative rounded-2xl p-5 w-min-[320px] h-min-[440px] w-[320px] h-[440px] flex flex-col justify-between bg-gradient-to-br from-[#23243a] to-[#18192b] border border-white/10 shadow-[0_4px_32px_0_rgba(0,0,0,0.40)] overflow-hidden"
    style="backdrop-filter: blur(16px)"
  >
    <div class="flex items-center justify-between z-10">
      <div class="flex items-center">
        <img
          :src="icon"
          :alt="`${name} icon`"
          class="w-9 h-9 rounded-lg bg-[#23243a] border border-[#35365a] mr-3"
        />
        <span class="text-white font-semibold text-lg">{{ name }}</span>
      </div>
      <button
        class="w-8 h-8 flex items-center justify-center rounded-lg bg-white/10 hover:bg-white/20 transition"
      >
        <svg
          width="18"
          height="18"
          fill="none"
          stroke="#fff"
          stroke-width="2"
          viewBox="0 0 24 24"
        >
          <path
            d="M9 6l6 6-6 6"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </button>
    </div>
    <img :src="preview" alt="" />
    <!-- Description -->
    <div class="mt-4 mb-2 z-10">
      <p class="text-white text-sm font-medium">{{ description }}</p>
    </div>

    <!-- Divider -->
    <div class="border-t border-white/10 my-3"></div>

    <!-- Preview image (optional, can be background or above options) -->
    <!-- <img :src="preview" :alt="`${name} preview`" class="w-full h-24 object-cover rounded-lg mb-3" /> -->
  </div>
</template>

<script setup>
defineProps({
  name: String,
  preview: String,
  icon: String,
  author: String,
  description: String,
});
</script>
