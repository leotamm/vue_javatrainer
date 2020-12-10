<template>
  <div id="questionsanswers" class="col-sm-12">
    <div class="offset">
      <table class="table table-bordered">
        <thead>
        <tr>
          <td>First Name</td>
          <td>Last Name</td>
          <td>User ID</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="p in displayedPosts">
          <td>{{p.first}}</td>
          <td>{{p.last}}</td>
          <td>{{p.suffix}}</td
        </tr>
        </tbody>
      </table>
</template>

<script>
export default {
  name: "QuestionsAnswers",
  data () {
    return {

    }
  },
  mehtods: {
    getAllQuestionsAndAnswers
  },
  computed: {

  }
}
</script>

<style scoped>
.offset{
  width: 500px !important;
  margin: 20px auto;
}
</style>