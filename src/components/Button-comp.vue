<template>
<button @click="affich()"
       :style="{ background:color}"
        class="btn"> {{text}}
</button>
</template>

<script>
export default {
  name: "Button-comp",
  props:{
    text: String,
    color: String,
  },
  methods: {
    affich(){
      this.$emit('btn-click')
      console.log('1')

    },
  },
}
</script>

<style scoped>

</style>