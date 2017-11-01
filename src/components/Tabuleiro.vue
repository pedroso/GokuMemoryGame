<template>
	<div style="padding: 5px; width: 700px; margin: 0 auto;">
    <div class="container-form">
      <button @click="resetCards()" class="btn btn-default">Recomeçar Jogo!</button>
    </div>

    <div v-for="carta in listaCartas" class="flip-container isLink" v-on:click="flipCard(carta)">
      <div class="flipper" :class="{flippered: carta.clicked}">
		    <carta :numero="carta.numero" :clicked="carta.clicked"></carta>
      </div>
    </div>
    <p>Tentativas: {{acertos + erros}} - Erros: {{erros}} - Acertos: {{acertos}}</p>

    <div class="container-form">
      <h1>Ranking dos Guerreiros</h1>
      <ul class="list-group" style="margin: 5px;">
        <li class="list-group-item" v-for="(item, index) in ranking">
          {{ index + 1 }} - <strong>Nome:</strong> {{ item.nome }} - <strong>Tentativas:</strong> {{ item.tentativas }}
        </li>
      </ul>

      <input type="button" @click="zerarRanking()" class="btn btn-warning" value="Zerar Ranking !" />
    </div>
	</div>
</template>

<script>
import db1Carta from './Carta'
import Vue from 'vue'

export default {
  name: 'tabuleiro',
  props: ['nivel', 'nome'],
  watch: {
    nivel: function (newVal, oldVal) {
      this.resetCards()
      this.setRanking()
    }
  },
  components: {
    'carta': db1Carta
  },
  created: function () {
    this.resetCards()
    this.setRanking()
  },
  data () {
    return {
      cards: [],
      flipeds: {itens: [], total: 0},
      flipping: false,
      acertos: 0,
      erros: 0,
      ranking: []
    }
  },
  methods: {
    flipCard: function (carta) {
      var cartaJogo = carta
      var me = this
      var flipeds = me.flipeds
      var clicouMesmaCarta = !!flipeds.itens[0] && flipeds.itens[0].id === cartaJogo.id
      if (!me.flipping && !clicouMesmaCarta && !cartaJogo.clicked) {
        cartaJogo.clicked = true
        if (flipeds.total === 0) {
          flipeds.total = flipeds.total + 1
          flipeds.itens.push(carta)
        } else {
          me.flipping = true
          if (flipeds.itens[0].numero === cartaJogo.numero) {
            flipeds.total = 0
            flipeds.itens = []
            me.flipping = false
            me.acertos = me.acertos + 1
            if (me.acertos === (me.cards.length / 2)) {
              setTimeout(function () {
                var resposta = confirm('Parabéns Guerreiro! Deseja jogar novamente?')
                me.rankearGuerreiro()
                if (resposta) {
                  me.resetCards()
                }
              }, 1000)
            }
          } else {
            me.erros = me.erros + 1
            setTimeout(function () {
              flipeds.itens[0].clicked = false
              cartaJogo.clicked = false
              flipeds.total = 0
              flipeds.itens = []
              me.flipping = false
            }, 2000)
          }
        }
      }
    },
    resetCards: function () {
      this.cards = []
      this.flipping = true
      var listaInicial = []
      this.acertos = 0
      this.erros = 0
      if (this.nivel === 'easy') {
        listaInicial = [
        { id: 1, numero: '03', clicked: false },
        { id: 2, numero: '01', clicked: false },
        { id: 3, numero: '04', clicked: false },
        { id: 4, numero: '05', clicked: false },
        { id: 5, numero: '02', clicked: false },
        { id: 6, numero: '01', clicked: false },
        { id: 7, numero: '02', clicked: false },
        { id: 8, numero: '03', clicked: false },
        { id: 9, numero: '04', clicked: false },
        { id: 10, numero: '05', clicked: false }]
      } else if (this.nivel === 'medium') {
        listaInicial = [
        { id: 1, numero: '01', clicked: false },
        { id: 2, numero: '02', clicked: false },
        { id: 3, numero: '03', clicked: false },
        { id: 4, numero: '04', clicked: false },
        { id: 5, numero: '05', clicked: false },
        { id: 6, numero: '06', clicked: false },
        { id: 7, numero: '07', clicked: false },
        { id: 8, numero: '08', clicked: false },
        { id: 9, numero: '09', clicked: false },
        { id: 10, numero: '10', clicked: false },
        { id: 11, numero: '01', clicked: false },
        { id: 12, numero: '02', clicked: false },
        { id: 13, numero: '03', clicked: false },
        { id: 14, numero: '04', clicked: false },
        { id: 15, numero: '05', clicked: false },
        { id: 16, numero: '06', clicked: false },
        { id: 17, numero: '07', clicked: false },
        { id: 18, numero: '08', clicked: false },
        { id: 19, numero: '09', clicked: false },
        { id: 20, numero: '10', clicked: false }]
      } else {
        listaInicial = [
        { id: 1, numero: '01', clicked: false },
        { id: 2, numero: '02', clicked: false },
        { id: 3, numero: '03', clicked: false },
        { id: 4, numero: '04', clicked: false },
        { id: 5, numero: '05', clicked: false },
        { id: 6, numero: '06', clicked: false },
        { id: 7, numero: '07', clicked: false },
        { id: 8, numero: '08', clicked: false },
        { id: 9, numero: '09', clicked: false },
        { id: 10, numero: '10', clicked: false },
        { id: 11, numero: '11', clicked: false },
        { id: 12, numero: '12', clicked: false },
        { id: 13, numero: '13', clicked: false },
        { id: 14, numero: '14', clicked: false },
        { id: 15, numero: '15', clicked: false },
        { id: 16, numero: '01', clicked: false },
        { id: 17, numero: '02', clicked: false },
        { id: 18, numero: '03', clicked: false },
        { id: 19, numero: '04', clicked: false },
        { id: 20, numero: '05', clicked: false },
        { id: 21, numero: '06', clicked: false },
        { id: 22, numero: '07', clicked: false },
        { id: 23, numero: '08', clicked: false },
        { id: 24, numero: '09', clicked: false },
        { id: 25, numero: '10', clicked: false },
        { id: 26, numero: '11', clicked: false },
        { id: 27, numero: '12', clicked: false },
        { id: 28, numero: '13', clicked: false },
        { id: 29, numero: '14', clicked: false },
        { id: 30, numero: '15', clicked: false }]
      }

      var listaFinal = listaInicial.sort(function () { var aleatorio = Math.random(); return aleatorio > Math.random() })
      this.cards = listaFinal
      this.desvirarCartas(listaFinal)
      this.listaCartas = listaFinal

      this.flipping = false
      return listaFinal
    },
    desvirarCartas: function (arrayCartas) {
      for (var i = arrayCartas.length - 1; i >= 0; i--) {
        arrayCartas[i].click = false
      }
    },
    rankearGuerreiro: function () {
      var ranking = Vue.ls.get('ranking', [])

      var tentativas = this.acertos + this.erros

      ranking.push({nome: this.nome, tentativas: tentativas, nivel: this.nivel})

      ranking.sort(function (a, b) { console.log('argumentos'); console.log(arguments); return a.tentativas > b.tentativas })

      Vue.ls.set('ranking', ranking)
      this.setRanking()
    },
    zerarRanking: function () {
      Vue.ls.set('ranking', [])
      this.ranking = Vue.ls.get('ranking', [])
    },
    setRanking: function () {
      var me = this
      var rankingNovo = Vue.ls.get('ranking', [])
      console.log(rankingNovo)
      rankingNovo = rankingNovo.filter(function (item) {
        return item.nivel === me.nivel
      })
      console.log(rankingNovo)
      this.ranking = rankingNovo.filter(function (item) {
        return item.nivel === me.nivel
      })
    }
  },
  computed: {
    listaCartas: {
      // getter
      get: function () {
        return this.cards
      },
      // setter
      set: function (listaCards) {
        this.cards = listaCards
      }
    }
  }
}
</script>


<style scoped>

.isLink {
  cursor: pointer;
}

.carta {
  width:116px; 
  height:116px; 
  display: inline-block;
}

.flip-container {
  -webkit-perspective: 1000;
  -moz-perspective: 1000;
  -o-perspective: 1000;
  perspective: 1000;
  display: inline-block; 
  border: 1px solid #ccc;
  margin: 1px;
}

.flippered {
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
  -o-transform: rotateY(180deg);
  transform: rotateY(180deg);
}

.flip-container, .front, .back {
  width: 116px;
  height: 116px;
}

.flipper {
  -webkit-transition: 0.6s;
  -webkit-transform-style: preserve-3d;

  -moz-transition: 0.6s;
  -moz-transform-style: preserve-3d;
  
    -o-transition: 0.6s;
  -o-transform-style: preserve-3d;

  transition: 0.6s;
  transform-style: preserve-3d;

  position: relative;
}

.front, .back {
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -o-backface-visibility: hidden;
  backface-visibility: hidden;

  position: absolute;
  top: 0;
  left: 0;
}

.front {
  background: url(../assets/img/back-carta.png) 0 0 no-repeat;
  background-size: 116px 116px;
  z-index: 2;
}

.back {
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
  -o-transform: rotateY(180deg);
  transform: rotateY(180deg);

  background: #f8f8f8;
}

.container-form {
  padding: 10px;
  margin-bottom: 10px;
}

</style>