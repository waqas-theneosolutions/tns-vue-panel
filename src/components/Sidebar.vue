<template>
  <aside
    :class="[
      'sidebar relative flex h-full flex-col transition-all duration-300',
      isCollapsed ? 'w-20' : 'w-72'
    ]"
  >
    <!-- Collapse/Expand Button -->
    <button
      @click="toggleSidebar"
      class="absolute -right-3 top-8 z-10 rounded-full border border-neutral-200 bg-white shadow-sm transition-shadow hover:shadow-md w-8 h-8"
    >
      <SvgIcon
        v-if="isCollapsed"
        size="24"
        name="expand" class="text-neutral-600" />
      <SvgIcon
        v-else
        size="24"
        name="collapse" class="text-neutral-600" />
    </button>

    <!-- Logo/Title Area -->
    <div class="mx-6 py-6">
      <div v-if="!isCollapsed" class="text-sidebar">
        <h2 class="text-xl font-bold">Admin</h2>
        <p class="mt-1 opacity-80">Business</p>
      </div>
      <div v-else class="flex justify-center">
        <div class="flex h-8 w-8 items-center justify-center rounded-lg bg-white">
          <span class="text-sm font-bold text-primary">A</span>
        </div>
      </div>
    </div>

    <!-- Navigation -->
    <nav class="sidebar-scrollbar flex-1 space-y-1 overflow-y-auto">
      <a
        v-for="item in navItems"
        :key="item.id"
        href="#"
        :class="[
          'sidebar-item group',
          item.active ? 'active' : '',
          isCollapsed ? 'justify-center px-3' : ''
        ]"
        :title="isCollapsed ? item.name : ''"
        @click="setActiveItem(item.id)"
      >
        <!-- Customer Icon -->
        <SvgIcon
          v-if="item.name === 'Customer Management'"
          size="24"
          name="people"
          class="h-5 w-5 flex-shrink-0" />

        <!-- Business Management Icon -->
        <SvgIcon
          v-else-if="item.name === 'Business Management'"
          size="24"
          name="briefcase" class="h-5 w-5 flex-shrink-0" />
        <!-- Support Icon -->
        <SvgIcon
          v-else-if="item.name === 'Support'"
          name="lifeguard"
          size="24"
          class="h-5 w-5 flex-shrink-0"          
        />
        <!-- Partners Icon -->
        <SvgIcon
          v-else-if="item.name === 'Partners/Galaxies'"
          class="h-5 w-5 flex-shrink-0"
          name="people"
          size="24"
        />
        <!-- Bookings Icon -->
        <SvgIcon
          v-else-if="item.name === 'Bookings'"
          class="h-5 w-5 flex-shrink-0"
          name="calendar"
          size="24"
        />
        <!-- Reports Icon -->
        <SvgIcon
          v-else-if="item.name === 'Reports'"
          class="h-5 w-5 flex-shrink-0"
          name="report"
        />
        <!-- Payments Icon -->
        <SvgIcon
          v-else-if="item.name === 'Payments'"
          name="payment"
          class="h-5 w-5 flex-shrink-0"
        />
        <!-- Settings Icon -->
        <SvgIcon
          name="setting"
          v-else-if="item.name === 'Settings'"
          class="h-5 w-5 flex-shrink-0"
        />

        <!-- Reviews Icon -->
        <SvgIcon
          name="star"
          v-else-if="item.name === 'Reviews'"
          class="h-5 w-5 flex-shrink-0"
        />
        <!-- Default Icon -->
        <SvgIcon
          v-else
          name="home"
          class="h-5 w-5 flex-shrink-0"
        />

        <span v-if="!isCollapsed" class="transition-opacity duration-200">
          {{ item.name }}
        </span>
        <span
          v-if="isCollapsed"
          class="pointer-events-none absolute left-full z-20 ml-2 whitespace-nowrap rounded bg-neutral-900 px-2 py-1 text-sm text-white opacity-0 transition-opacity group-hover:opacity-100"
        >
          {{ item.name }}
        </span>
      </a>
    </nav>

    <!-- User Profile (Sticky to Bottom) -->
    <div class="sticky bottom-6 mt-6 p-5" v-show="!isCollapsed">
      <div class="sidebar-profile flex items-center gap-3 rounded-lg p-3">
        <div
          class="sidebar-profile-initials flex h-10 w-10 items-center justify-center rounded-full"
        >
          <span class="font-semibold">JD</span>
        </div>
        <div class="min-w-0 flex-1">
          <p class="truncate font-medium text-white">John Doe</p>
          <p class="truncate text-sm text-white opacity-80">Admin</p>
        </div>

        <!-- Three-dot menu button -->
        <div class="relative">
          <button
            @click="toggleProfileMenu"
            class="flex h-8 w-8 items-center justify-center rounded-md text-white transition-colors hover:bg-white/20"
          >
            <SvgIcon
              name="dotted"
              class="h-5 w-5"
            />
          </button>

          <!-- Dropdown Menu -->
          <div
            v-if="showProfileMenu"
            class="absolute bottom-full right-0 z-50 mb-2 w-48 rounded-lg border border-neutral-200 bg-white py-1 shadow-lg"
          >
            <!-- Profile Info -->
            <div class="border-b border-neutral-100 px-4 py-3">
              <p class="font-medium text-neutral-900">John Doe</p>
              <p class="text-sm text-neutral-500">john.doe@example.com</p>
            </div>

            <!-- Menu Items -->
            <button
              @click="handleMenuClick('profile')"
              class="flex w-full items-center gap-3 px-4 py-3 text-left text-neutral-700 transition-colors hover:bg-neutral-50"
            >
              <SvgIcon
                name="profile"
                class="h-5 w-5 text-neutral-500"
              />
              <span>My Profile</span>
            </button>

            <button
              @click="handleMenuClick('account')"
              class="flex w-full items-center gap-3 px-4 py-3 text-left text-neutral-700 transition-colors hover:bg-neutral-50"
            >
              <SvgIcon
                name="setting"
                class="h-5 w-5 text-neutral-500"
              />
              <span>Account Settings</span>
            </button>

            <button
              @click="handleMenuClick('help')"
              class="flex w-full items-center gap-3 px-4 py-3 text-left text-neutral-700 transition-colors hover:bg-neutral-50"
            >
              <SvgIcon
                name="help"
                class="h-5 w-5 text-neutral-500"
              />
              <span>Help & Support</span>
            </button>

            <div class="my-1 border-t border-neutral-100"></div>

            <button
              @click="handleMenuClick('logout')"
              class="flex w-full items-center gap-3 px-4 py-3 text-left text-error transition-colors hover:bg-error-light"
            >
              <SvgIcon
                name="out"
                class="h-5 w-5"
              />
              <span>Logout</span>
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Click outside to close menu -->
    <div v-if="showProfileMenu" class="fixed inset-0 z-40" @click="(showProfileMenu = false)"></div>
  </aside>
</template>

<script setup lang="ts">
  import { ref, computed, onMounted, onUnmounted } from 'vue'
  import SvgIcon from './SvgIcon/SvgIcon.vue'

  const isCollapsed = ref(false)
  const showProfileMenu = ref(false)
  const activeNavItem = ref(1)

  const toggleSidebar = () => {
    isCollapsed.value = !isCollapsed.value
    // Close profile menu when collapsing sidebar
    if (isCollapsed.value) {
      showProfileMenu.value = false
    }
  }

  const toggleProfileMenu = () => {
    showProfileMenu.value = !showProfileMenu.value
  }

  const setActiveItem = (id: number) => {
    activeNavItem.value = id
  }

  const handleMenuClick = (action: string) => {
    showProfileMenu.value = false
    console.log('Menu action:', action)

    switch (action) {
      case 'profile':
        alert('Opening profile page...')
        break
      case 'account':
        alert('Opening account settings...')
        break
      case 'help':
        alert('Opening help & support...')
        break
      case 'logout':
        if (confirm('Are you sure you want to logout?')) {
          alert('Logging out...')
        }
        break
    }
  }

  // Close menu when clicking outside
  const closeMenuOnClickOutside = (event: MouseEvent) => {
    if (showProfileMenu.value && !(event.target as HTMLElement).closest('.relative')) {
      showProfileMenu.value = false
    }
  }

  // Close menu when pressing Escape key
  const closeMenuOnEscape = (event: KeyboardEvent) => {
    if (event.key === 'Escape' && showProfileMenu.value) {
      showProfileMenu.value = false
    }
  }

  // Add event listeners
  onMounted(() => {
    document.addEventListener('click', closeMenuOnClickOutside)
    document.addEventListener('keydown', closeMenuOnEscape)
  })

  // Remove event listeners
  onUnmounted(() => {
    document.removeEventListener('click', closeMenuOnClickOutside)
    document.removeEventListener('keydown', closeMenuOnEscape)
  })

  const navItems = computed(() => [
    { id: 1, name: 'Customer Management', active: activeNavItem.value === 1 },
    { id: 2, name: 'Business Management', active: activeNavItem.value === 2 },
    { id: 3, name: 'Support', active: activeNavItem.value === 3 },
    { id: 4, name: 'Partners/Galaxies', active: activeNavItem.value === 4 },
    { id: 5, name: 'Bookings', active: activeNavItem.value === 5 },
    { id: 6, name: 'Reports', active: activeNavItem.value === 6 },
    { id: 7, name: 'Payments', active: activeNavItem.value === 7 },
    { id: 8, name: 'Settings', active: activeNavItem.value === 8 },
    { id: 9, name: 'Reviews', active: activeNavItem.value === 9 }
  ])
</script>

<style scoped>
  /* No need for custom styles here as they're in style.css */
</style>
