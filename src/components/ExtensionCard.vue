<template>
  <div
    class="relative bg-gray-800 rounded-xl shadow-md p-4 flex flex-col items-center text-center w-full max-w-xs min-h-[420px] border-2 border-transparent hover:bg-gray-700/80 transition-all duration-300 group"
    style="box-shadow: 0 0 8px 1px #60a5fa22"
  >
    <div
      class="absolute inset-0 rounded-xl pointer-events-none border-2 border-blue-300 opacity-30 group-hover:opacity-50"
      style="z-index: 0; box-shadow: 0 0 8px 2px #60a5fa33"
    ></div>
    <img
      :src="preview"
      :alt="`${name} preview`"
      class="w-full h-auto object-cover rounded-lg mb-3 relative z-10"
    />
    <div class="flex justify-center flex-col items-center relative z-10 pt-6">
      <div class="flex items-center mb-2 relative z-10">
        <img :src="icon" :alt="`${name} icon`" class="w-8 h-8 rounded mr-2" />
        <span class="text-lg font-semibold text-white">{{ name }}</span>
      </div>
      <div class="text-sm text-gray-400 mb-1 relative z-10">
        by {{ author }}
      </div>
      <p class="text-gray-300 text-sm relative z-10">{{ description }}</p>
    </div>
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
