<template>
  <div>
    
  </div>
  <Word/>
</template>

<script>
import Word from '@/components/Word.vue'
export default {
  name: 'Login',
  components: {
    Word
  },
  props: {

  },
  data() {
    return {
      message: 'La word es: ',
    }
  },
  mounted() {
    console.log('algo');
    //this.getWords();
  },
  methods:{
    getWords: function (){
      return null
    }
  },
}
</script>

<style scoped>

</style>