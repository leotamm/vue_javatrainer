<template>
  <div class="about">
    <h1>Welcome to javaTrainer</h1>
    <h2>Student view</h2>
    <input v-model.name="studentName" placeholder="Sisesta nimi" type="text">
    <p>
      <button v-on:click="getName()">Genereeri test</button>
    </p>
  </div>

</template>


<script>

let getName = function () {
  this.$http.get = ("http://localhost:8090/trainer/testpackage",
      {
        params: {
          questionSet: this.questionSet
        }
      })
      .then(result => this.questionSet = result.data)
      .then(displayQuestions(questionSet))
}



export default {
  name: 'javaTrainer',
  methods: {
    getName: getName
    /*    register: registerFunction,
        showResponse: showResponse,
        test: test,
        getData: getData,
        deleteRow: deleteRow

     */
  },
  data: function () {
    return {
      studentName: '',
      questionSet: {}
    }
  },
  created() {
    this.getName()
  }
}
</script>


<style>

</style>