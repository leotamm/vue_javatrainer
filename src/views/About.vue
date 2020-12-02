<template>

  <div class="about">
    <h1>Welcome to javaTrainer</h1>
    <h2>Student view</h2>
    <input v-model.name="studentName" placeholder="Sisest nimi" type="text">
    <p>
      <button v-on:click="getName()" :disabled="isDisabled" @click="changeSet('show')">GENEREERI TEST</button>
    </p>


    <table width="450px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff"
           v-for="(a, index) in questionSet">
      <tr class=default v-bind:class="{correct: a.correct, notcorrect: !a.correct && hasSubmitButton=== true}">
        <td>Küsimus teemast {{ index + 1 }}: <br> <h4>{{ a.question }}</h4>              <div style="color: blue" ></div></td>
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

    <p v-if="state === 'show'">
      <button v-on:click="submit()" >SAADA VASTUSED</button>
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
<!--    {{ resultList }}-->
    <br>

<!--    {{questionSet}}-->
    <div id="tulemus">
     <h2>{{score}}</h2>

<!--      {{row.questionId}}-->
    </div>


<!--    <div v-for="row in resultList.answers">-->
<!--      Sinu tulemus on : {{resultList.totalResult.testScore}} %-->
<!--      &lt;!&ndash;      {{row.questionId}}&ndash;&gt;-->
<!--    </div>-->

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
  this.hasSubmitButton = true;
  let url = "http://localhost:8090/trainer/submitAnswer";
  let requestBody = {studentName: this.studentName, resultObject: []};
  for (let i = 0; i < this.questionSet.length; i++) {
    requestBody.resultObject.push({questionId: this.questionSet[i].q_id, answerId: this.questionSet[i].selectedAnswer});
    //push lisab lõppu ühe elemendi

  }

  this.$http.post(url, requestBody)
      .then(result => {
          this.resultList = result.data
          this.score = "Sinu tulemus on : " + this.resultList.totalResult.testScore + "% !"
          for(let i = 0; i < this.resultList.answers.length; i++){
            this.questionSet[i].correct  =this.resultList.answers[i].correct;
          }
      })






}


export default {
  name: 'javaTrainer',
  methods: {
    getName: getName,
    submit: submit,
    changeSet: function(newState){
      this.state = newState
    }

  },
  data: function () {
    return {
      state: 'hide',
      studentName: '',
      questionSet: {},
      resultList: {},
      isDisabled: false,
      score: '',
      hasSubmitButton: false

    }
  },

}
</script>


<style>
.default {
  background-color: cornsilk;

}
  .correct{
    background-color: #d3ff8f;
  }
  .notcorrect {
    background-color: #ffc8c8;
  }

</style>