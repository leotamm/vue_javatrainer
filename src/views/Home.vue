<template>
  <div class="home" style="background-color:#efeaf0">
    <br>
    <img alt="School Logo" width="100" src="../assets/school-icon_2.png">
    <WelcomePage message="Tere tulemast javaTrainerit kasutama!"/>
    <br>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import WelcomePage from '@/components/WelcomePage'

export default {
  name: 'Home',
  components: {
    HelloWorld,
    WelcomePage
  }
}
</script>
