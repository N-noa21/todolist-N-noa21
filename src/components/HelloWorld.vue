<script setup lang="ts">
import ClickCounter from './ClickCounter.vue'
import ItemList from './ItemList.vue'
import TodoList from './TodoList.vue';

defineProps<{
  msg: string
}>()
</script>

<template>
  <div>
    <TodoList />
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>