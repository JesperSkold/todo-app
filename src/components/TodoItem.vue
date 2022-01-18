<template>
	<li><input type="checkbox" @change="$emit('checkHandler', todo)" />{{ todo.name }} <span class="material-icons" @click="$emit('deleteTodo', todo.id)"> delete </span></li>
	<!-- change so you dont directly manipulate the prop todo.done = !todo.done -->
</template>

<script>
export default {
	props: {
		todo: Object,
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
