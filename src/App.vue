<template>
	<div id="app">
		<TodoMenu :todoItems="todoItems" @hideDone="hideDones" @showDone="showAgain" @deleteDone="deleteDones" @clearData="clearLocal"/>
		<section></section>
		<p>Du har {{  checkTodoLength }} todos kvar att göra</p>
		<TodoList :todos="todoItems" @addTodo="saveItem" @checkHandler="echo" />
		<h2 v-if="error">Please enter a valid todo</h2>
		<button @click="lol = !lol">hehe</button>
		<h1 v-if="lol">test</h1>
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
			lol: false,
			todoItems: [],
			showDone: true,
			error: false,
		};
	},
		computed: {
			checkTodoLength(){
				let todoLength = 0;
				for (const elem of this.todoItems) {
					if (!elem.done) {
						todoLength++
					}
				}
					return todoLength
			}
		},
	methods: {
		echo(todo){
			todo.done = !todo.done
		},
		saveItem(item) {
			if (!item || item.match(/^\s/)) {
				this.error = true;
			} else {
				this.error = false;
				this.todoItems.push({ id: this.newId(), name: item, done: false });
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
			}
		},
		newId() {
			return Math.random().toString(16).slice(2);
		},
		hideDones(){
			this.todoItems = this.todoItems.filter(x => x.done === false)
		},
		showAgain() {
			this.todoItems = JSON.parse(localStorage.getItem("localItems"));
		},
		deleteDones(){
			this.todoItems = this.todoItems.filter(x => x.done === false)
			localStorage.setItem("localItems", JSON.stringify(this.todoItems));
		},
		clearLocal(){
			this.todoItems = []
			localStorage.clear()
		}
	},

	created() {
		if (localStorage.localItems) {
			this.todoItems = JSON.parse(localStorage.getItem("localItems"));
		}
	},
};
</script>
<style>
*{
	margin: 0;
	padding: 0;
}
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
</style>
