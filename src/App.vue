<template>
	<div id="app">
		<TodoMenu :todoItems="todoItems" @hideDone="hideDones" @showDone="showAgain" @deleteDone="deleteDones" @clearData="clearLocal" />
		<section></section>
		<p>Du har {{ checkTodoLength }} todos kvar att göra</p>
		<TodoList :todos="todoItems" @addTodo="saveItem" @checkHandler="echo" @deleteTodo="deleteTodo" />
		<h2 v-if="error">Please enter a valid todo</h2>
	</div>
</template>

<script>
import TodoMenu from "./components/TodoMenu.vue";
import TodoList from "./components/TodoList.vue";
export default {
	components: {
		TodoMenu,
		TodoList,
	},
	data() {
		return {
			todoItems: [],
			showDone: true,
			error: false,
		};
	},
	computed: {
		checkTodoLength() {
			let todoLength = 0;
			for (const elem of this.todoItems) {
				if (!elem.done) {
					todoLength++;
				}
			}
			return todoLength;
		},
	},
	methods: {
		echo(todo) {
			todo.done = !todo.done;
		},
		deleteTodo(todo) {
			for (const key in this.todoItems) {
				if (this.todoItems[key].id === todo) {
					this.todoItems.splice(key, 1)
				}
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
			}
			// console.log(todo);
			// let i = this.todoItems.map(item => item.id)
			// console.log(Object.values(this.todoItems));
			// console.log(Object.values(this.todoItems).indexOf(todo));
			// this.todoItems.splice(this.todoItems.indexOf(todo), 1);
			// this.todoItems.$remove(todo, 1)
		},
		saveItem(item) {
			if (!item || item.match(/^\s/)) {
				this.error = true;
			} else {
				this.error = false;
				this.todoItems = JSON.parse(localStorage.getItem("localItems"));
				this.todoItems.push({ id: this.newId(), name: item, done: false });
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
			}
		},
		newId() {
			return Math.random().toString(16).slice(2);
		},
		hideDones() {
			this.todoItems = this.todoItems.filter((x) => x.done === false);
		},
		showAgain() {
			this.todoItems = JSON.parse(localStorage.getItem("localItems"));
		},
		deleteDones() {
			this.todoItems = this.todoItems.filter((x) => x.done === false);
			localStorage.setItem("localItems", JSON.stringify(this.todoItems));
		},
		clearLocal() {
			this.todoItems = [];
			localStorage.clear();
		},
	},

	created() {
		if (localStorage.localItems) {
			this.todoItems = JSON.parse(localStorage.getItem("localItems"));
		}
	},
};
</script>
<style>
* {
	margin: 0;
	padding: 0;
}
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
</style>
