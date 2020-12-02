<template>

  <div class="about">
    <h1>Welcome to javaTrainer</h1>
    <h2>Student view</h2>
    <input v-model.name="studentName" placeholder="Sisest nimi" type="text">
    <p>
      <button v-on:click="getName()" :disabled="isDisabled">GENEREERI TEST</button>
    </p>


    <table width="450px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff"
           v-for="(a, index) in questionSet">
      <tr>
        <td>Küsimus {{ index + 1 }}: {{ a.question }}</td>
      </tr>

      <tr>
        <div v-for="b in a.answers">

          <td>
            <table width="430px">{{ b.answer }}</table>
          </td>
          <td><input id="radio1" type="radio" v-model="a.selectedAnswer" v-bind:value="b.answerId" v-bind:name="index">
          </td>
        </div>
      </tr>

    </table>

    <p>
      <button v-on:click="submit()">SAADA VASTUSED</button>
    </p>
<!--
    <table width="450px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff"
           v-for="(a, index) in resultList">
      <tr>
        <td>
          <table width="430px">{{ a.testScore }}</table> indeksil 7 ???
        </td>
      </tr>
    </table>

        {{ questionSet }}  -->
    {{ resultList }}
    <div v-for="row in resultList.answers">
      {{row.questionId}}
    </div>
<!--    {{resultList.totalResult.testScore}}-->
    <br><br>
  </div>
</template>

<script>

let getName = function () {
  this.$http.get("http://localhost:8090/trainer/testpackage")
      .then(result => this.questionSet = result.data)
  this.isDisabled = true;

}
let submit = function () {

  let url = "http://localhost:8090/trainer/submitAnswer";
  let requestBody = {studentName: this.studentName, resultObject: []};

  for (let i = 0; i < this.questionSet.length; i++) {
    requestBody.resultObject.push({questionId: this.questionSet[i].q_id, answerId: this.questionSet[i].selectedAnswer});
    //push lisab lõppu ühe elemendi

  }

  this.$http.post(url, requestBody)
      .then(result => this.resultList = result.data)


}


export default {
  name: 'javaTrainer',
  methods: {
    getName: getName,
    submit: submit

  },
  data: function () {
    return {
      studentName: '',
      questionSet: {},
      resultList: {},
      isDisabled: false


    }
  },

}
</script>


<style>

</style>