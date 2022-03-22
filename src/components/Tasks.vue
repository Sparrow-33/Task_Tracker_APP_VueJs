<template>
 <div :key="task.id" v-for="task in tasks">
   <Task_single
       @toggle-reminder="$emit('toggle-reminder',task.id)"
       @delete-task="$emit('delete-task',task.id)" :task="task"/>
 </div>

</template>

<script>
import Task_single from "@/components/Task"

export default {
  name: "Tasks_Comp",
  props:{
    tasks:Array,
  },
  components: {
    Task_single
  },
  emits:['delete-task','toggle-reminder'],

}
</script>

<style scoped>

</style>