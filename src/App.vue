<template>
  <ListComponent :list-data="myList" :visibleItems="5" :index="currentIndex">
    <template #default="{ item }">
      <div>{{ item.name }}</div>
    </template>
  </ListComponent>
</template>

<script setup>
import { ref } from 'vue';
import ListComponent from './CustomList.vue'; // Assuming the above component is saved as ListComponent.vue

const myList = ref([
  {name: 'Item 1'},
  {name: 'Item 2'},
  {name: 'Item 3'},
  {name: 'Item 4'},
  {name: 'Item 5'},
  {name: 'Item 6'},
]);

const currentIndex = ref(0);

// Example: Change the index after 2 seconds
setTimeout(() => {
  currentIndex.value = 2;
}, 2000);
</script>
