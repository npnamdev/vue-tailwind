<template>
  <div class="h-[100vh] w-full flex justify-center items-center">
    <div class="relative">
      <button ref="dropdownButton" @click="toggleDropdown" class="bg-[#717ae3] px-4 py-1.5 rounded w-full text-white">Profile</button>
      <ul v-if="isOpen" :class="[dropdownPositionClass]" class="cursor-pointer mt-1.5 flex flex-col px-5 py-2 w-[170px] ring-1 ring-gray-200 rounded-md shadow-lg bg-white absolute">
        <li v-for="(item, index) in dropdownItems" :key="index" @click="handleItemClick(item)" class="h-[30px] flex items-center">
          <span v-if="item.icon" class="mr-2">
            <i :class="item.icon"></i>
          </span>
          {{ item.label }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const isOpen = ref(false);
const dropdownPosition = ref('bottom-right');
const dropdownButton = ref(null);

onMounted(() => {
  dropdownButton.value.offsetHeight;
});

const toggleDropdown = () => {
  isOpen.value = !isOpen.value;
};

const dropdownItems = [
  { label: 'Profile' },
  { label: 'Edit', icon: 'i-heroicons-pencil-square-20-solid', click: () => { console.log('Edit') } },
  { label: 'Duplicate', click: () => { console.log('Duplicate') } },
  { label: 'Delete', click: () => { console.log('Delete') } }
];

const dropdownPositionClass = computed(() => {
  const offsetHeight = dropdownButton.value.offsetHeight;
  switch (dropdownPosition.value) {
    case 'bottom-right':
      return `top-[${offsetHeight}px] right-0`;
    case 'bottom-left':
      return `top-[${offsetHeight}px] left-0`;
    default:
      return `top-[${offsetHeight}px] right-0`;
  }
});

const handleItemClick = (item) => {
  if (item.click) {
    item.click();
  }
  toggleDropdown();
};
</script>
