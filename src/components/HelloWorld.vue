<template>
  <div class="hello" style="width: 100%;">

    <div class="jumbotron">
      <div class="container">
        <img src="../assets/img/back-goku.gif" width="250" style="border-radius: 10px 40px;border: 3px solid #444;" />
        <h1>{{ msg }}</h1>
        <h2>Antes de começar o desafio, digite seu nome!</h2>
      </div>
    </div>
    <div class="container-form">
      <label>Nome:</label>
      <input type="text" name="nome" v-model="nome" />
    </div>

    <div v-show="!!nome">
      <div class="container-form">
        <p>Selecione o seu nível!</p>
        <input type="radio" id="easy" name="level" value="easy" v-show="false" v-model="nivel" checked="checked" />
        <label for="easy"><img src="../assets/img/nivel1.png" width="100" height="100" v-bind:class="{ isLink: true, selected: nivel == 'easy', unselected: nivel != 'easy' }"/></label>

        <input type="radio" id="medium" name="level" value="medium" v-show="false" v-model="nivel"/>
        <label for="medium"><img src="../assets/img/nivel2.png" width="100" height="100" v-bind:class="{ isLink: true, selected: nivel == 'medium', unselected: nivel != 'medium' }" /></label>

        <input type="radio" id="hard" name="level" value="hard" v-show="false" v-model="nivel"/>
        <label for="hard"><img src="../assets/img/nivel3.png" width="100" height="100" v-bind:class="{ isLink: true, selected: nivel == 'hard', unselected: nivel != 'hard' }" /></label>
        
      </div>
      
      <h3>Sayajin nível {{fraseDoNivel()}}</h3>

      <tabuleiro :nivel="nivel" :nome="nome"></tabuleiro>
    </div>
  </div>
</template>

<script>
import db1Tabuleiro from './Tabuleiro'

export default {
  name: 'HelloWorld',
  components: {
    'tabuleiro': db1Tabuleiro
  },
  methods: {
    fraseDoNivel: function () {
      return this.nivel === 'easy' ? '1' : this.nivel === 'medium' ? '2' : '3'
    }
  },
  data () {
    return {
      msg: 'Olá guerreiro sayajin, eu sou o Goku!',
      nome: '',
      nivel: 'easy',
      oldNivel: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1, h2 {
  font-weight: normal;
}

.isLink {
  cursor: pointer;
}

.selected {
  border: 3px solid #000;
}

.unselected {
  border: 3px solid #CCC;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.container-form {
  padding: 10px;
  margin-bottom: 10px;
}
</style>
