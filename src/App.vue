<template>
  <div class="app">
    <div class="container py-5">
      <div class="row justify-content-center">
        <div class="col-6">
          <todo-table />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import TodoTable from '@/components/TodoTable.vue'

</script>

<style lang="scss" scoped>
.todo-wrapper {
  background-color: $white;
}
</style>
