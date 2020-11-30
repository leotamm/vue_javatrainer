<template>
  <div class="about">
    <h1>Welcome to javaTrainer</h1>
    <h2>Student view</h2>
    <input v-model.name="studentName" placeholder="Sisesta nimi" type="text">
    <p>
      <button v-on:click="getName()">Genereeri test</button>
    </p>

    <table width="500px" align="centre" border="1" v-for="(a, index) in questionSet">
      <tr><td>Küsimus {{index+1}}: {{ a.question }}</td></tr>
      <tr>
      <div v-for="b in a.answers">

        <td>{{ b.answer }}</td>
          <td><input id="radio1" type="radio" v-model="a.selectedAnswer" v-bind:value="b.answerId" v-bind:name="index"></td>

      </div>
      </tr>
    </table>
  {{questionSet}}
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