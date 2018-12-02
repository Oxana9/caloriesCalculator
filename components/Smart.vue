<template>
	<div class='smart'>
		<h2>Smart</h2>
		<label>Enter your age</label>
		<InputNumber type='number'  placeholder='Enter your age' v-model='age'></InputNumber>
		<Input type='text' placeholder='Male or famale?' v-model='sex'></Input>
		<p>
			<span>You are free to eat  </span>
			<span>{{resultCalories}}</span>
			<span>calories today!</span>
		</p>
		<nuxt/>
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