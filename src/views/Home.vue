<template>
  <div class="home" style="background-color:#efeaf0">
    <br>
    <img alt="School Logo" width="100" src="../assets/school-icon_2.png">
    <WelcomePage message="Tere tulemast javaTrainerit kasutama!"/>
    <br>
  </div>
</template>

<script>
import WelcomePage from '@/components/WelcomePage'

export default {
  name: 'Home',
  components: {
    WelcomePage
  }
}
</script>
