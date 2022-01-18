<template>
	<li>
		<input type="checkbox" :checked="alreadyChecked" @change="$emit('checkHandler', todo)" />{{ todo.name }}
		<span class="material-icons" @click="$emit('deleteTodo', todo.id)"> delete </span>
	</li>
	<!-- change so you dont directly manipulate the prop todo.done = !todo.done -->
</template>

<script>
export default {
	props: {
		todo: Object,
	},
	mounted() {
		// for (const key in this.todo) {
		if (this.todo.done === true) {
			this.alreadyChecked = true;
			// }
		}
	},
	data() {
		return {
			alreadyChecked: false,
		};
	},
};
</script>

<style lang="scss" scoped>
li {
	background: papayawhip;
	list-style: none;
	margin: 1rem;
	input {
		margin: 2rem;
	}
}
</style>
