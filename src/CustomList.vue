<template>
  <div ref="root" :style="{ height: `${visibleItems * itemHeight}px`, overflowY: 'auto' }">

    <ul ref="list">
      <li>Hard coded </li>
      <li v-for="(item, index) in listData" :key="index">
        <slot :item="item" :index="index">{{ item }}</slot>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue';

// Props for the component
const props = defineProps({
  listData: {
    type: Array,
    required: true,
  },
  visibleItems: {
    type: Number,
    required: true,
  },
  index: {
    type: Number,
    default: 0,
  },
});

// References to DOM elements
const root = ref(null);
const list = ref(null);
const itemHeight = ref(0);

// Set up the item height and scroll the list to the correct index on mount
onMounted(() => {
  if (list.value && list.value.firstChild) {
    itemHeight.value = list.value.firstChild.clientHeight;
  }
  scrollToIndex(props.index);
});

// Watch for changes in the index prop and scroll the list
watch(() => props.index, (newIndex) => {
  scrollToIndex(newIndex);
});

// Function to scroll to the correct index
function scrollToIndex(index) {
  if (root.value && itemHeight.value > 0) {
    root.value.scrollTop = index * itemHeight.value;
  }
}
</script>

<style scoped>
/* Basic styles */
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px; /* Assume all items have the same height, or adjust accordingly */
  border-bottom: 1px solid #ccc;
}
</style>
