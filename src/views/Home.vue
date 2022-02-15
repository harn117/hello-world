<template class="container">
  <div class="container">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Prueba de desarrollo Vue y Laravel"/>
  </div>

</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/Word.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
