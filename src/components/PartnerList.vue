<template>
  <div class="card">
    <h3 class="mb-4 font-medium">Partner List</h3>
    <div class="space-y-4">
      <div
        v-for="partner in partners"
        :key="partner.id"
        class="flex items-center gap-3 rounded-lg p-3 hover:bg-gray-50"
      >
        <div class="flex h-10 w-10 items-center justify-center rounded-full bg-blue-100">
          <span class="font-semibold text-blue-600">{{ partner.initials }}</span>
        </div>
        <div>
          <p class="font-medium text-gray-900">{{ partner.name }}</p>
          <p class="text-sm text-gray-500">{{ partner.role }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  const partners = [
    { id: 1, name: 'Beauty Aesthetic', role: 'John Doe', initials: 'BA' },
    { id: 2, name: 'Beauty Aesthetic', role: 'John Doe', initials: 'BA' },
    { id: 3, name: 'Beauty Aesthetic', role: 'John Doe', initials: 'BA' },
    { id: 4, name: 'Beauty Aesthetic', role: 'John Doe', initials: 'BA' }
  ]
</script>
