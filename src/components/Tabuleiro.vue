<template>
	<div style="padding: 5px; width: 700px; margin: 0 auto;">
		<carta v-for="numeroCarta in listaCartas" :numero="numeroCarta"></carta>
	</div>
</template>

<script>
import db1Carta from './Carta'

export default {
  name: 'tabuleiro',
  props: ['nivel'],
  components: {
    'carta': db1Carta
  },
  data () {
    return {
      nome: 'Goku'
    }
  },
  computed: {
    listaCartas: function () {
      var listaInicial = []

      if (this.nivel === 'easy') {
        listaInicial = ['01', '02', '03', '04', '05']
      } else if (this.nivel === 'medium') {
        listaInicial = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10']
      } else {
        listaInicial = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15']
      }

      var listaFinal = listaInicial.concat(listaInicial).sort(function () { var aleatorio = Math.random(); return aleatorio > Math.random() })

      return listaFinal
    }
  }
}
</script>