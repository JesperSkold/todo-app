<template>
	<li v-show="!hideOrShowChecked">
		<input type="checkbox" :checked="alreadyChecked" @change="$emit('checkHandler', todo)" />
		<p>{{ todo.name }}</p>
		<span class="material-icons" @click="$emit('deleteTodo', todo.id)"> delete </span>
	</li>
</template>

<script>
export default {
	props: {
		todo: Object,
		hideChecks: Boolean,
	},
	mounted() {
		if (this.todo.done === true) {
			this.alreadyChecked = true;
		}
	},
	data() {
		return {
			alreadyChecked: false,
		};
	},
	computed: {
		hideOrShowChecked() {
			if (this.todo.done === true && this.hideChecks === true) {
				return true;
			}
			return false;
		},
	},
};
</script>

<style lang="scss" scoped>
li {
	font-size: 1.3rem;
	gap: 1rem;
	display: flex;
	width: 90%;
	background: rgba(75, 75, 74, 0.404);
	list-style: none;
	margin: 0.4rem 0;
	span {
		align-self: center;
		cursor: pointer;
		margin-left: auto;
	}
	input {
		align-self: center;
		transform: scale(2);
		margin: 1rem;
	}
	p {
		padding: 1rem;
		overflow-wrap: anywhere;
	}
}
</style>
