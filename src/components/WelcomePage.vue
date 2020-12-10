<template>
  <div class="hello">
    <h2>{{ message }}</h2>
  </div>
</template>

<script>
export default {
  name: 'WelcomePage',
  props: {
    message: String,
    message2: String
  }
}
</script>

<style scoped>
h1{
  color: #197815
}
h2{
  color:darkgrey;
}
</style>

