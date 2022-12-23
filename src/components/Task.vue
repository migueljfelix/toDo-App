<template>
  <div 
    @click="$emit('toggle-completed', task.id)/* emit for toggle on app component */"  
    :class="[task.completed ? 'completed' : '', 'task']"> <!-- if task is completed add completed to classes -->
    <h3>{{ task.description }}</h3>
    <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i> <!-- emit event to eliminate data from app component-->
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
.task { // task ui
  background-color: rgba(246, 255, 247, 0.3);
  border-radius: 8px;
  margin: 12px 0px;
  padding: 8px 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task.completed { // completed background
  background-color: rgba(29, 139, 38, 0.459);
}
.fas { // delete button
  color: rgb(39, 39, 39);
}
</style>
