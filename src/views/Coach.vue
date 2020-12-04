<template>

  <div class="about">
    <h1>Hei, õpetaja!</h1> <!-- peale sisselogimist, kuvame kujul "Hei, [nimi]!" -->

    <p><button v-on:click="getResultList" >VAATA TULEMUSI</button></p>

    <ul align="centre">
      <h3> <a href="http://localhost:8090/" target="_blank" rel="noopener">Küsimuste sisestamine andmebaasi</a> </h3>
    </ul>

    <table width="750px" align="centre" style="margin: 0px auto;" border="1" bgcolor="#f0f8ff">
      <tr class=default>
        <td> <h4>Testi tulemused:</h4>              <div style="color: blue" ></div></td>
      </tr>

      <tr>
        <div v-for="(a, index) in resultSet">

          <td width="100px">
            {{a.resultId}}
          </td>
          <td width="250px"> {{a.name}}
          </td>

          <td width="100px"> {{a.result}}   %
          </td>

          <td width="250px"> {{ (a.timestamp) }}
          </td>
        </div>
      </tr>

    </table>
<!--{{resultSet}}-->
  </div>
</template>

<script>

let getResultList = function () {
  this.$http.get("http://localhost:8090/trainer/getresults")
      .then(result => this.resultSet = result.data)

}

export default {
  name: 'Coach',
  methods: {
    getResultList: getResultList

  },
  data: function () {
    return {
      resultSet: {},
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