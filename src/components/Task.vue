<template>
  <div
    @click="$emit('toggle-completed', task.id)"
    :class="[task.completed ? 'completed' : '', 'task']"
  >
    <h3>{{ task.description }}</h3>
    <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
  </div>
</template>
<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>
<style lang="scss" scoped>
.task {
  background-color: rgba(246, 255, 247, 0.3);
  border-radius: 8px;
  margin: 5px 0px;
  padding: 10px 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task.completed {
  background-color: rgba(25, 163, 36, 0.3);
}
.fas {
  color: red;
}
</style>
