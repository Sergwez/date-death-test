<template>
  <div>
    <FirstPage v-if="!$route.query.step"/>
    <Quizz v-else/>
  </div>
</template>
<script>
import FirstPage from '@/components/FirstPage.vue'
import Quizz from '../components/Quiz.vue'
export default {
  components:{
    FirstPage,
    Quizz
  }

}
</script>
<style scoped>

</style>