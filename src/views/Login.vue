<template>
  <div class="login">
    <h2>Logi sisse:</h2>
    <input type="text" name="username" v-model="input.username" placeholder="Kasutajanimi"/><br><br>
    <input type="password" name="password" v-model="input.password" placeholder="Parool"/><br><br>
    <button type="button" v-on:click="login()">Logi sisse</button>
    <p><button v-on:click="logout()">Logi välja</button></p>
<!--    <h5>{{ response }}</h5>   -->
    <br><br><br><br>
    <h2>Loo uus kasutaja:</h2>
    <input type="text" name="newuser" v-model="input2.newuser" placeholder="Kasutajanimi"/><br><br>
    <input type="password" name="newpassword" v-model="input2.newpassword" placeholder="Parool"/><br><br>
    <button type="button" v-on:click="create()">Loo uus kasutaja</button><br>
<!--    <h5>{{ response2 }}</h5>    -->
  </div>
</template>


<script>
export default {
  name: 'Login',
  data: function () {
    return {
      state: 'hide',
      response: '',
      response2: '',
      input: {
        username: '',
        password: ''
      },
      input2: {
        newuser: '',
        newpassword: ''
      },
      // loginName: ''
    }
  },

  methods: {
    login: function () {
      if (this.input.username === "" && this.input.password === "") {
        alert("Sisselogimisel peavad nimi ja parool olema sisestatud!");
      } else {
        let url = "http://localhost:8090/trainer/login"
        let requestBody = {
          userName: this.input.username,
          userPassword: this.input.password,
          userClass: ''
        }
        this.$http.post(url, requestBody)
            .then(result => {
              this.response = result.data
              localStorage.setItem('user-token', result.data)
              localStorage.setItem('username', this.input.username)
              this.$http.defaults.headers.common['Authorization'] = "Bearer " + result.data
              location.reload()
              alert('Sisse logitud!')
            })
      }
    },
    logout() {
      localStorage.removeItem('user-token')
      localStorage.removeItem('username')
      localStorage.removeItem('list-length')
      location.reload()
      alert("Välja logitud!")
    }
    ,
    create() {
      if (this.input2.newuser === "" && this.input2.newpassword === "") {
        alert("Uue kasutaja nimi ja parool olema sisestatud!");
      } else {
        let url = "http://localhost:8090/trainer/newUser"
        let requestBody = {
          userName: this.input2.newuser,
          userPassword: this.input2.newpassword,
          userClass: 'user'
        }
        //console.log(requestBody)
        this.$http.post(url, requestBody)
            .then(result => {
              this.response2 = result.data
              location.reload()
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