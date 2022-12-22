<template lang="">

    <div :key="task.id" v-for="task in tasks"> <!-- loop, for each task in Tasks output something -->
        <Task
      @toggle-completed="$emit('toggle-completed', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
    </div>
</template>
<script>

import Task from "./Task"
export default {
        name: "Tasks",
        props:{
            tasks: Array,
        },    
    components:{
        Task,
    },
    emits:["toggle-completed", "delete-task"]
    
}
</script>
<style lang="">
    
</style>