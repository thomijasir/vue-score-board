<template>
	<div class="counter">
		<div class="column">
			<button @click="Decrese()">-</button>
		</div>
		<div class="column">
			<input type="number" v-model="count" class="column-input"/>
		</div>
		<div class="column">
			<button @click="Increse()">+</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Counter',
	props: ['id','funcUpdate'],
	data () {
		return {
			count: 1
		}
	},
	methods: {
		Increse(){
			this.count += 1
		},

		Decrese(){
			if(this.count <= 1){
				this.count = 1
			} else {
				this.count -= 1
			}
		}
	},
	watch:{
		count(value){
			// console.log('Has change!: ', value)
			const newObject = {
				idCounter: this.id,
				valCounter: value,
			}
			this.funcUpdate(newObject)
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.counter{
	display: flex;
}
.column-input{
	width: 2rem;
	text-align: center;
}
input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
  margin: 0; 
}
</style>
