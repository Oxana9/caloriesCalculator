<template>
<Container>
  <Header>
	<h1>Calories calculator</h1>
  </Header>
  <Container>
    <Aside width="200px">	
		<div class='choice'>
			<p>What you choose?</p>
			<Button type="primary" plain v-on:click="visible=!visible">{{visible?'Smart calculator':'Simple calculator'}}</Button>
		</div>
	</Aside>
    <Main>
		<div v-if='visible'>
			<Simple :value="products" :resultCalories='resultCalories' />
		</div>
		<div v-else>
			<Smart :value="products" :resultCalories='resultCalories' />
		</div>
	</Main>
  </Container>
</Container>
</template>

<script>
import ElementUIComponents from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import Smart from '../components/Smart.vue'
import Simple from '../components/Simple.vue'

export default {
	components: {
		...ElementUIComponents,
		Smart,
		Simple
	},
        data () {
			return {
			visible: true,
			simpleFood: '',
			simpleGrams: '',
			newFood: '',
            foods: [], 
			simple: '',
			sex: '',
			age: '',
			male: false,
			female: false,
			products: [
                {name:'Milk', calories:64},
                {name:'Cheeze', calories:220}, 
                {name:'Ananas', calories:49},
                {name:'Cabbage', calories:27},
                {name:'Egg', calories:157}]
        }
		},
		methods: {
			getCalories: function() {
			if(this.age==''||this.sex!='male'&&this.sex!='female'){
				return "a lot";
			}
				if(this.sex=='male'){
					if(this.age<=18){
						return 1500;
					}
					if(this.age<=40){
						return 3000;
					}
					if(this.age<=60){
						return 2800;
					}
					return 2400;
				}
				if(this.age<=18) {
					return 1300;
				}
				if(this.age<=40){
					return 2800;
				}
				if(this.age<=60){
					return 2400;
				}
				return 2200;
			},
			getFoodCalories: function(food) {
				var calories = 0;
				this.products.forEach(function(product){
					if(product.name==food.simpleFood) {
						calories = product.calories;
					}
				});
				return food.simpleGrams * calories / 100;
			},
			getDailyCalories() {
				var entireCalories = 0;
				this.foods.forEach(function(food){
					entireCalories += this.getFoodCalories(food);
				}.bind(this));
				return entireCalories;
			},
			
		},
		computed: {
			resultCalories: function() {
				var result = this.getCalories()-this.getDailyCalories();
				if(!isNaN(result)) {
					if(result>0) {
						return result;
					}
					return 'nothing else for ';
				} 
				return 'a lot of ';
			}
		}
	}
</script>