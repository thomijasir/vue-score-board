<template>
	<div class="hello">
		<h1>Learn Vue Comunication In Looping</h1>
		<table>
			<thead>
				<tr>
					<th>ID</th>
					<th>Name</th>
					<th>Winstreak</th>
					<th>Total Score</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item in person" :key="item.index">
					<td>{{item.id}}</td>
					<td>{{item.name}}</td>
					<td><Counter :id="item.id" :funcUpdate="updateScore"/></td>
					<td>{{item.score}}</td>
				</tr>
				<tr v-show="addPlayerActive">
					<td><input type="number" placeholder="Enter ID" v-model="idPlayer"></td>
					<td><input type="text" placeholder="Enter Name" v-model="namePlayer"></td>
					<td>-</td>
					<td><input type="number" placeholder="Enter Current Score" v-model="currentScore"></td>
				</tr>
			</tbody>
			<tfoot>
				<tr>
					<td>
						<button @click="addPlayer()">{{addPlayerActive ? 'Save Player' : 'Add Player'}}</button>
						<button @click="cancelPlayer()" v-show="addPlayerActive">Cancel</button>
					</td>
					<td colspan="2">Total Score All Player</td>
					<td>{{totalScores}}</td>
				</tr>
			</tfoot>
		</table>
	</div>
</template>

<script>
import Counter from './Counter'

function add(a, b) {
    return a + b;
}


export default {
	name: 'scoreBoard',
	components: {
		Counter,
	},
	data () {
		return {
			addPlayerActive: false,
			idPlayer: '',
			namePlayer: '',
			currentScore: '',
			person:[
				{
					id: 1,
					name: 'Thomi',
					score: 120,
				},
				{
					id: 2,
					name: 'Bobby',
					score: 335,
				},
				{
					id: 3,
					name: 'Farhan',
					score: 780,
				},
				{
					id: 4,
					name: 'Rozi',
					score: 450,
				},
			]
		}
	},
	computed:{
		totalScores(){
			const getScore = this.person.map(el => el.score).reduce((a, b) => a + b, 0);
			return getScore
		}
	},
	methods:{
		addPlayer(){
			this.addPlayerActive = !this.addPlayerActive
			if(!this.addPlayerActive){
				const newPlayerObject = {
					id: this.idPlayer,
					name: this.namePlayer,
					score: parseInt(this.currentScore),
				}
				this.person.push(newPlayerObject)
				console.log('Person Data: ', this.person)
				this.resetForm()
			}
		},
		cancelPlayer(){
			this.resetForm()
		},
		resetForm(){
			this.idPlayer = ''
			this.namePlayer = ''
			this.currentScore = ''
			this.addPlayerActive = false
		},
		updateScore(value){
			const items = this.person.map(element => element.id)
			const index = items.indexOf(value.idCounter);
			if (~index) {
				const multiply = this.person[index].score * value.valCounter
				this.person[index].score = multiply;
			}
			console.log('GET index ', index)
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
table, td, th {
    border: 1px solid #ddd;
    text-align: left;
}

table {
    border-collapse: collapse;
    width: 70%;
	margin-left: auto;
	margin-right: auto;
}

th, td {
    padding: 15px;
}
input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
  margin: 0; 
}
</style>
