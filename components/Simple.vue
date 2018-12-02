<template>
	<div class='simple'>
		<h2>Simple</h2>
		<label for='food'>What have you had today?</label>
		<Select name='food' v-model='simpleFood' placeholder='Food'>
			<Option v-for="product in products" v-bind:value="product.name">
				{{ product.name }}
			</Option>
		</Select>
		<InputNumber type='number' placeholder='Enter the quantity of your meal in gramms' v-model='simpleGrams'></InputNumber>
		<Button type="primary" plain v-on:click="foods.push({simpleFood:simpleFood, simpleGrams:simpleGrams})">Add</Button>
		<div v-if="simpleFood">
			<p>Today you had: {{getDailyCalories()}}</p>
			<p>
				<ul>
					<li v-for="(food, index) in foods">{{food.simpleFood}} {{food.simpleGrams}} gramms is {{getFoodCalories(food)}} calories
						<Button type="danger" plain v-on:click="foods.splice(index, 1)">Delete</Button>
					</li>
				</ul>
			</p>
		</div>
	</div>
</template>

<script>
import ElementUIComponents from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

export default {
	components: {
		...ElementUIComponents
	},
	props: {
		value: null,
		resultCalories: null
	},
	data(){
		return {
			age: '',
			sex: ''
		}
	}
}
</script>