<template>
  <div class="card">
    <h3 class="mb-4 font-medium">Filters</h3>
    <div class="space-y-3">
      <label class="flex cursor-pointer items-center gap-3">
        <input
          type="checkbox"
          class="h-4 w-4 rounded border-gray-300 text-blue-600"
          v-model="looksPartners"
        />
        <span class="text-gray-700">Looks Partners</span>
      </label>

      <label class="flex cursor-pointer items-center gap-3">
        <input
          type="checkbox"
          class="h-4 w-4 rounded border-gray-300 text-blue-600"
          v-model="businessOwner"
        />
        <span class="text-gray-700">Business Owner</span>
      </label>

      <label class="flex cursor-pointer items-center gap-3">
        <input
          type="checkbox"
          class="h-4 w-4 rounded border-gray-300 text-blue-600"
          v-model="viewOnly"
        />
        <span class="text-gray-700">View</span>
      </label>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const looksPartners = ref(false)
  const businessOwner = ref(false)
  const viewOnly = ref(false)
</script>
