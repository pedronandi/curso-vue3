<template>
  <h1>Lifecycle Hooks</h1>
</template>

<script>
import { onMounted } from 'vue'

export default {
  setup() {
    onMounted(() => {
      console.log('Foi montado composition API!')
    })
  }
  
  /*mounted() {
    console.log('Foi montado options API!')
  }*/
}
</script>