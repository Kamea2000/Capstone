<script setup>
import { ref } from 'vue';
import { Link } from '@inertiajs/vue3';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';


// State management for sidebar and dropdown
const sidebarOpen = ref(false);
const patientsDropdownOpen = ref(false);

// Functions to toggle state
const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value;
};

const togglePatientsDropdown = () => {
  patientsDropdownOpen.value = !patientsDropdownOpen.value;
};

const toggInventoryDropdown = () => {
  patientsDropdownOpen.value = !patientsDropdownOpen.value;
};
</script>

<template>
  <div class="relative flex">
    <!-- Hamburger Menu (Mobile) -->
    <button @click="toggleSidebar" class="p-4 block lg:hidden fixed top-0 left-0 z-50">
      <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
      </svg>
    </button>

    <!-- Sidebar -->
    <div
      class="fixed top-0 left-0 h-screen w-48 bg-white text-gray-800 p-5 transform transition-transform lg:translate-x-0 lg:block"
      :class="{ '-translate-x-full': !sidebarOpen }"
    >
      <!-- Logo -->
      <div class="flex text-bold items-center justify-center mb-10">
        <img :src="ApplicationLogo" alt="Logo" class="h-12 w-auto" />
        <span>HSO</span>
      </div>

      <!-- Navigation -->
      <nav class="flex flex-col space-y-2">
        <Link href="/dashboard" class="block py-2.5 px-4 rounded hover:bg-gray-100 flex items-center"
          :class="{ 'bg-gray-100': $page.component === 'Dashboard' }">
          <font-awesome-icon :icon="['fas', 'home']" class="mr-3" /> Dashboard
        </Link>

        <!--Users-->
        <Link href="/user" class="block py-2.5 px-4 rounded hover:bg-gray-100 flex items-center"
          :class="{ 'bg-gray-100': $page.component === 'User' }">
          <font-awesome-icon :icon="['fas', 'heartbeat']" class="mr-3" /> Users
        </Link>

        <!--Patients-->
        <Link href="/patient-list" class="block py-2.5 px-4 rounded hover:bg-gray-100 flex items-center"
          :class="{ 'bg-gray-100': $page.component === 'PatientList' }">
          <font-awesome-icon :icon="['fas', 'heartbeat']" class="mr-3" /> Patient List
        </Link>

        <!-- Patients Dropdown -->
        <div>
          <button @click="togglePatientsDropdown" class="w-full flex justify-between py-2.5 px-4 rounded hover:bg-green-100 hover:text-black transition duration-200">
            <div class="flex items-center">
              <font-awesome-icon :icon="['fas', 'clipboard']" class="mr-3" />
              <span :class="{ 'font-semibold': $page.component.startsWith('Patients') }">Inventory</span>
            </div>
            <font-awesome-icon :icon="['fas', 'chevron-right']" :class="{ 'rotate-90': patientsDropdownOpen }" class="transition-transform" />
          </button>

          <!-- Collapsible Links -->
          <div v-if="patientsDropdownOpen" class="pl-6 space-y-2">
            <Link href="/inventory/category" class="block py-2.5 px-4 rounded hover:bg-green-100 flex items-center"
              :class="{ 'bg-gray-100': $page.component === 'IndividualTreatmentRecord' }">
              <font-awesome-icon :icon="['fas', 'clipboard']" class="mr-3" /> Category
            </Link>
            <Link href="/inventory/products" class="block py-2.5 px-4 rounded hover:bg-green-100 flex items-center"
              :class="{ 'bg-gray-100': $page.component === 'PrenatalPostpartum' }">
              <font-awesome-icon :icon="['fas', 'heartbeat']" class="mr-3" /> Products
            </Link>
          </div>
        </div>

        <Link href="/appointments" class="block py-2.5 px-4 rounded hover:bg-gray-100 flex items-center"
          :class="{ 'bg-gray-100': $page.component === 'Mortality' }">
          <font-awesome-icon :icon="['fas', 'user']" class="mr-3" /> Appointments
        </Link>

        <Link href="/sales" class="block py-2.5 px-4 rounded hover:bg-gray-100 flex items-center"
          :class="{ 'bg-gray-100': $page.component === 'Mortality' }">
          <font-awesome-icon :icon="['fas', 'user']" class="mr-3" /> Sales
        </Link>
      </nav>
    </div>

    <!-- Overlay (Mobile) -->
    <div v-if="sidebarOpen" @click="toggleSidebar" class="fixed inset-0 bg-black opacity-50 lg:hidden"></div>

    <!-- Main Content -->
    <div class="flex-1 p-5 lg:ml-48">
      <slot />
    </div>
  </div>
</template>

<style scoped>
/* Optional styles */
</style>
