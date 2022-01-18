<template>
	<li>
		<input type="checkbox" :checked="alreadyChecked" @change="$emit('checkHandler', todo)" />
    <p>{{ todo.name }}</p>
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
  font-size: 1.7rem;
	gap: 1rem;
	display: flex;
  flex-wrap: wrap;
	align-items: center;
	width: 35rem;
  min-height: 8rem;
	background: papayawhip;
	list-style: none;
	margin: 0.4rem 0;
  span{
    padding: 1rem;
    margin-left: auto;
  }

	input {
    transform: scale(2);
		margin: 1rem;
	}
}
</style>
