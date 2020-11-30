<template>
  <div class="about">
    <h1>Welcome to javaTrainer</h1>
    <h2>Student view</h2>
    <input v-model.name="studentName" placeholder="Sisesta nimi" type="text">
    <p>
      <button v-on:click="getName()">Genereeri test</button>
    </p>
    <div v-for="a in questionSet">
      Question q_id: {{a.q_id}}
      Question question: {{a.question}}
      <div v-for="b in a.answers">
        Answer answerId: {{b.answerId}}
        Answer answer: {{b.answer}}
      </div>
    </div>
  </div>

</template>


<script>

let getName = function () {
  this.$http.get("http://localhost:8090/trainer/testpackage")
      .then(result => this.questionSet = result.data)

}

export default {
  name: 'javaTrainer',
  methods: {
    getName: getName

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