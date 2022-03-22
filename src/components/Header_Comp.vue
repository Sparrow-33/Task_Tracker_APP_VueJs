<template>
  <header>
    <h1>This is a header</h1>
    <Button text="Add Task" color="green"/>


  </header>
</template>

<script>
import Button from './Button-comp'

 export default {
   // eslint-disable-next-line vue/multi-word-component-names
  name: 'Header_Comp',
  props:{
    title : String,
  } ,
   components:{
    Button
   }
}
</script>

<style scoped>
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>