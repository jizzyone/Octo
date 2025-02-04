<script>
export default {
  name: "Card",
  props: {
    category: String,
    image: String,
    author: String,
    title: String,
    description: String
  }
}
</script>

<template>
  <div class="rounded shadow">
    <div class="relative w-full" style="max-height: 192px;">
      <img :src="image" class="w-full h-48 object-cover rounded-t">
      <span class="absolute top-4 left-4 px-3 py-1 text-white text-sm"
            :class="category === 'DEVELOPMENT' ? 'bg-blue-700' : 'bg-cyan-500'">
        CATEGORY | {{ category }}
      </span>
    </div>
    <div class="p-4 md:p-6">
      <p class="text-cyan-500 mb-2">{{ author }}</p>
      <h3 class="text-xl font-bold mb-2">{{ title }}</h3>
      <p class="text-gray-600 mb-4">{{ description }}</p>
      <button class="text-white px-4 py-2 rounded hover:opacity-90 transition-opacity"
              :class="category === 'DEVELOPMENT' ? 'bg-blue-700' : 'bg-cyan-500'">
        Call to action
      </button>
    </div>
  </div>
</template>

<style scoped>

</style>