<template>

  <div class="login">
    <h2>Logi sisse:</h2>
    <input type="text" name="username" v-model="input.username" placeholder="Kasutajanimi"/>
    <br>
    <br>
    <input type="password" name="password" v-model="input.password" placeholder="Parool"/>
    <br>
    <br>
    <button type="button" v-on:click="login()">Logi sisse</button>
    <br><br><br><br>
    <h2>Tee uus kasutaja:</h2>
    <input type="text" name="newuser" v-model="input2.username" placeholder="Kasutajanimi"/>
    <br>
    <br>
    <input type="password" name="newpassword" v-model="input2.password" placeholder="Parool"/>
    <br>
    <br>
    <button type="button" v-on:click="create()">Loo uus kasutaja</button>


  </div>

</template>

<script>


export default {
  name: 'Login',
  data() {
    return {
      input: {
        username: "",
        password: ""
      },
      input2: {
        username: "",
        password: ""
      }
    }
  },
  methods: {
    login() {
      if (this.input.username === "" && this.input.password === "") {
        console.log("Kasutajanimi ja parool peavad mõlemad olema sisestatud!");
      }
      else {
        console.log("testtest"); //siia viide POST funktsioonile
      }
    },
    create() {
      if (this.input.username === "" && this.input.password === "") {
        console.log("Kasutajanimi ja parool peavad mõlemad olema sisestatud!");
      }
      else {
        console.log("testtest2"); //siia viide POST funktsioonile
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