<template>
<div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder':
              '','task']">
  <h3>{{task.text}}
    <i @click="$emit('delete-task',task.id)" class="fa-solid fa-xmark"></i>
  </h3>
  <p>{{task.day}}</p>
</div>
</template>

<script>
export default {
  name: "Task_single",
  props:{
    task:Object
  },
  methods:{
    onDelete(id){
      this.$emit('delete-task', id)
    },
  },

}
</script>

<style scoped>
 .fa-solid{
   color: red;
 }

 .task{
   background: #d8eafc;
   margin: 5px;
   padding: 10px 20px;
   cursor: pointer;
 }
 .task.reminder{
   border-left: 5px solid #3664a8;
 }
 .task h3{
   display: flex;
   align-items: center;
   justify-content: space-between;
 }
</style>