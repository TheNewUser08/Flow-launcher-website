<script setup>
defineProps({
  title: String,
  description: String,
  alt: String,
  icon: [Object, Function], // Accepts a component
});
</script>

<template>
  <div class="flex flex-col items-center text-center p-4">
    <div v-if="icon" class="mb-2">
      <component :is="icon" class="w-8 h-8 mx-auto" />
    </div>

    <h3 class="text-xl font-semibold mb-2">{{ title }}</h3>
    <p class="text-gray-400">{{ description }}</p>
  </div>
</template>

<style scoped></style>
