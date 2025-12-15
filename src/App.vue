<template>
  <div class="grid min-h-screen grid-cols-1 bg-gray-50 lg:grid-cols-[auto_1fr]">
    <!-- Sidebar -->
    <Sidebar />

    <!-- Main Content Area -->
    <div class="overflow-auto">
      <div class="p-8">
        <header class="mb-8">
          <h1 class="text-2xl font-bold text-gray-900">Support</h1>
        </header>

        <!-- Business & Customers Support Section -->
        <section class="mb-8">
          <div class="mb-6 flex flex-col justify-between gap-4 sm:flex-row sm:items-center">
            <h2 class="text-lg font-semibold text-gray-800">Business & Customers Support</h2>
            <div class="w-full sm:w-64">
              <SearchInput />
            </div>
          </div>

          <div class="grid grid-cols-1 gap-6 lg:grid-cols-2">
            <!-- Filters Section -->
            <div class="space-y-4">
              <CheckboxGroup />
              <PartnerList />
              <Heading />
            </div>

            <!-- Business List -->
            <BusinessList />
          </div>
        </section>

        <hr class="my-8 border-gray-300" />

        <!-- Demo Components Section -->
        <section class="mb-8">
          <FormDemo />
        </section>
      </div>
    </div>

    <!-- Dialog (initially hidden) -->
    <SupportDialog v-if="showDialog" @close="(showDialog = false)" />

    <!-- Floating Action Button -->
    <button
      @click="(showDialog = true)"
      class="fixed bottom-6 right-6 z-10 rounded-full bg-primary p-4 text-white shadow-lg transition-colors hover:bg-primary-700"
    >
      <svg
        class="h-6 w-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
      </svg>
    </button>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import Sidebar from './components/Sidebar.vue'
  import SearchInput from './components/SearchInput.vue'
  import CheckboxGroup from './components/CheckboxGroup.vue'
  import PartnerList from './components/PartnerList.vue'
  import BusinessList from './components/BusinessList.vue'
  import FormDemo from './components/FormDemo.vue'
  import SupportDialog from './components/SupportDialog.vue'
  import Heading from './components/Heading.vue'

  const showDialog = ref(false)
</script>
