<template>
	<div class="flip-container isLink" v-on:click="flipCard"  >
		<div class="flipper" :class="{flippered: this.clicked}">
			<div class="front">
	      		
		    </div>
		    <div class="back">
				<div class="carta">
					<img :src="imagePath()" />
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'carta',
  props: ['numero'],
  methods: {
    imagePath: function () {
      return require('../assets/img/' + this.numero + '.png')
    },
    flipCard () {
      var me = this
      me.clicked = true

      window.setTimeout(function () {
        me.clicked = false
      }, 2000)
    }
  },
  data () {
    return {
      clicked: false
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

</style>