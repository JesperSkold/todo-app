<template>
	<section>
		<ul>
			<TodoItem v-for="item in todos" :key="item.id" :todo="item" @checkHandler="childEcho" @deleteTodo="deleteTodo" :hideChecks="hideChecks"/>
		</ul>
		<article class="form">
			<!-- make this form-->
			<input
				type="text"
				v-model="inputValue"
				@keyup.enter="
					$emit('addTodo', inputValue);
					inputValue = '';
				"
			/>
			<button
				@click="
					$emit('addTodo', inputValue);
					inputValue = '';
				"
			>
				Lägg till todo
			</button>
		</article>
	</section>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
	props: {
		todos: Array,
    hideChecks: Boolean
	},
	components: { TodoItem },
	data() {
		return {
			inputValue: null,
		};
	},
	methods: {
		childEcho(todo) {
			this.$emit("checkHandler", todo);
		},
		deleteTodo(todo) {
			this.$emit("deleteTodo", todo);
		},
	},
};
</script>

<style lang="scss" scoped>
button {
	color: white;
	background: rgba(0, 0, 0, 0.883);
	font-size: 1.8rem;
	height: 4rem;
	width: 25rem;
}
input {
	text-align: center;
	font-size: 2rem;
	width: 25rem;
	height: 4rem;
}
.form {
	margin-top: 1rem;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
ul {
	height: 35rem;
	overflow-y: scroll;
	display: flex;
	flex-direction: column;
	align-items: center;
}
</style>
