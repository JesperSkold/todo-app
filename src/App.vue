<template>
	<div id="app">
		<TodoMenu :todoItems="todoItems" @hideDone="hideDones" @deleteDone="deleteDones" @clearData="clearLocal" />
		<section class="intro">
			<img src="./assets/teflon-panna.svg" alt="" />
			<h1>TEFLON</h1>
			<p>När det inte fastnar</p>
		</section>
		<p class="length">
			Du har <b>{{ checkTodoLength }}</b> todos kvar att göra
		</p>
		<TodoList :todos="todoItems" @addTodo="saveItem" @checkHandler="echo" @deleteTodo="deleteTodo" :hideChecks="hideChecks"/>
		<h2 v-if="error">Please enter a valid todo</h2>
		<h2 v-if="errorLength">Your todo can not be longer than 50 characters</h2>
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
			hideChecks: null,
			todoItems: [],
			showDone: true,
			error: false,
			errorLength: false,
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
			localStorage.setItem("localItems", JSON.stringify(this.todoItems));
		},
		deleteTodo(todo) {
			for (const key in this.todoItems) {
				if (this.todoItems[key].id === todo) {
					this.todoItems.splice(key, 1);
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
			} else if (item.length > 50) {
				this.errorLength = true;
			} else {
				this.error = false;
				this.errorLength = false;
				if (localStorage.localItems) {
					this.todoItems = JSON.parse(localStorage.getItem("localItems"));
				}
				this.todoItems.push({ id: this.newId(), name: item, done: false });
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
			}
		},
		newId() {
			return Math.random().toString(16).slice(2);
		},
		hideDones(bool) {
			this.hideChecks = bool
			// this.todoItems = this.todoItems.filter((x) => x.done === false);
			// console.log(this.todoItems.filter((x) => x.done === true));
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
<style lang="scss">
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
* {
	margin: 0;
	padding: 0;
}
body {
	margin: auto;
	width: 40%;
	height: 100vh;
}
.intro {
	margin-top: .5rem;
	display: flex;
	flex-direction: column;
	align-items: center;
	h1 {
		margin: 0.8rem;
		font-size: 3rem;
	}
	img {
		transform: scale(2);
	}
}
.length {
	margin: 4rem 0 2rem 0;
	text-align: center;
	b {
		font-size: 1.2rem;
	}
}
#app h2{
	margin: .5rem;
	text-align: center;
}
</style>
