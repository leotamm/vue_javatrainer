<template>

  <div class="login">
    <h2>Logi sisse:</h2>
    <input type="text" name="username" v-model="input.username" placeholder="Kasutajanimi"/><br><br>
    <input type="password" name="password" v-model="input.password" placeholder="Parool"/><br><br>
    <button type="button" v-on:click="login()">Logi sisse</button>
    <br><br><br><br>
    <h2>Loo uus kasutaja:</h2>
    <input type="text" name="newuser" v-model="input2.newuser" placeholder="Kasutajanimi"/><br><br>
    <input type="password" name="newpassword" v-model="input2.newpassword" placeholder="Parool"/><br><br>
    <button type="button" v-on:click="create()">Loo uus kasutaja</button>
    <div>{{ response }}</div>
  </div>

</template>

<script>

export default {
  name: 'Login',
  data: function () {
    return {


      response: '',
      input: {
        username: '',
        password: ''
      },
      input2: {
        newuser: '',
        newpassword: ''
      },
    }
  },

  methods: {
    login() {
      if (this.input.username === "" && this.input.password === "") {
        console.log("Sisselogimisel peavad nimi ja parool olema sisestatud!");
      } else {
        console.log("testtest"); //siia viide POST funktsioonile
      }
    },
    create() {
      if (this.input.newuser === "" && this.input.newpassword === "") {
        console.log("Uue kasutaja nimi ja parool olema sisestatud!");
      } else {
        let url = "http://localhost:8090/trainer/newUser"
        let requestBody = {
            userName: this.input2.newuser,
            userPassword: this.input2.newpassword,
            userClass: 'user'
        }
        console.log(requestBody)
        this.$http.post(url, requestBody)
            .then(result => {
              this.response = result.data
              alert('Kasutaja loodud!')
            })
      }
    }
  }
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