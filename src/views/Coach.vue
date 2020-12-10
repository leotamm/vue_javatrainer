<template>


  <div>
    <div class="about" style="background-color:#efeaf0">
      <h1>Hei, õpetaja!</h1>
      <p><button v-on:click="getResultList">VAATA TULEMUSI</button></p>
      <p><button v-on:click="getQuestionsAndAnswers">KÜSIMUSTE ANDMEBAAS</button></p>
    <ul align="centre"><h3><a href="http://localhost:8090/" target="_blank" rel="noopener">Küsimuste sisestamine
      andmebaasi</a></h3></ul>
    </div><br>
    <table v-if="resultsState === 'show'" width="550px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff">
      <table border="1">
        <tr>
          <td width="100px"><h4 v-on:click="sort('r_l_id')">Nr</h4></td>
          <td width="180px"><h4 v-on:click="sort('student_id')">Nimi</h4></td>
          <td width="100px"><h4 v-on:click="sort('result')">Tulemus</h4></td>
          <td width="250px"><h4 v-on:click="sort('timestamp')">Aeg</h4></td>
        </tr>
      </table>
      <tr>
        <div v-for="(a, index) in resultSet">
          <td width="100px">{{ a.resultId }}</td>
          <td width="180px"> {{ a.name }}</td>
          <td width="100px"> {{ a.result }} %</td>
          <td width="250px"> {{ (a.timestamp) }}</td>
        </div>
      </tr>
    </table>

    <table v-if="questionsState === 'show'" width="800px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff">
      <table border="1">
        <tr>
          <td width="100px"><h4>Teema</h4></td>
          <td width="350px"><h4>Küsimus</h4></td>
          <td width="350px"><h4>Vastus</h4></td>
          <td width="100px"><h4>Õige/vale</h4></td>
        </tr>
      </table>
      <tr>
        <div v-for="(a, index) in fullSet">
          <td width="100px">{{ a.topicId }}</td>
          <td width="350px"> {{ a.question }}</td>
          <td width="350px"> {{ a.answer }}</td>
          <td width="100px"> {{ (a.correct) }}</td>
        </div>
      </tr>
    </table>



  </div>

</template>

<script>
//import QuestionsAnswers from "@/components/QuestionsAnswers";

let getQuestionsAndAnswers = function () {
  this.questionsState = 'show'
  this.resultsState = 'hide'
  this.$http.get('http://localhost:8090/trainer/getall')
      .then(result => this.fullSet = result.data)

}

let sort = function (column) {
  this.$http.get('http://localhost:8090/trainer/getresults', {
        params: {
          column: column,
          direction: this.direction
        }
      }
  ).then(result => this.resultSet = result.data)
  if (this.direction === 'ASC') {
    this.direction = 'DESC'
  } else {
    this.direction = 'ASC'
  }
}

let getResultList = function () {
  this.resultsState = 'show'
  this.questionsState = 'hide'
  this.$http.get("http://localhost:8090/trainer/getresults")
      .then(result => this.resultSet = result.data)
  localStorage.setItem('list-length', this.resultSet.length)
}

export default {
  name: 'Coach',

  data: function () {
    return {
      resultSet: {},
      fullSet: {},
      resultsState: 'hide',
      questionsState: 'hide',
      direction: 'ASC',
      r_l_id: null,
      student_id: null,
      result: null,
      timestamp: null,
    }
  },
  methods: {
    getResultList: getResultList,
    sort: sort,
    getQuestionsAndAnswers: getQuestionsAndAnswers
  },
}
</script>


<style>
.default {
  background-color: cornsilk;
}
.correct {
  background-color: #d3ff8f;
}
.notcorrect {
  background-color: #ffc8c8;
}
</style>