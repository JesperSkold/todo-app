<template>
	<div id="app">
		<TodoMenu :todoItems="todoItems" @hideDone="hideDones" @deleteDone="deleteDones" @clearData="clearLocal" />
		<section class="intro">
			<img src="./assets/teflon-panna.svg" alt="" />
			<h1>TEFLON</h1>
			<p>When it doesn't stick</p>
		</section>
		<p class="length">
			You have <b>{{ checkTodoLength }}</b> todos left.
		</p>
		<p :class="{ showChecksInfo: hideChecks, hideChecksInfo: !hideChecks }"></p>
		<TodoList :todos="todoItems" @addTodo="saveItem" @checkHandler="echo" @deleteTodo="deleteTodo" :hideChecks="hideChecks" />
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
			hideChecks: null,
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
			localStorage.setItem("localItems", JSON.stringify(this.todoItems));
		},
		deleteTodo(todo) {
			for (const key in this.todoItems) {
				if (this.todoItems[key].id === todo) {
					this.todoItems.splice(key, 1);
				}
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
			}
		},
		saveItem(item) {
				if (localStorage.localItems) {
					this.todoItems = JSON.parse(localStorage.getItem("localItems"));
				}
				this.todoItems.push({ id: this.newId(), name: item, done: false });
				localStorage.setItem("localItems", JSON.stringify(this.todoItems));
		},
		newId() {
			return Math.random().toString(16).slice(2);
		},
		hideDones(bool) {
			this.hideChecks = bool;
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
	overflow-x: hidden;
}
.intro {
	margin-top: 0.5rem;
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
	margin: 4rem 0 0 0;
	text-align: center;
	b {
		font-size: 1.2rem;
	}
}
#app h2 {
	margin: 0.5rem;
	text-align: center;
}

.hideChecksInfo::after {
	content: "(Showing done todos)";
	display: block;
	text-align: center;
	margin: 0 0 1rem 0;
}
.showChecksInfo::after {
	content: "(Hiding done todos)";
	display: block;
	text-align: center;
	margin: 0 0 1rem 0;
}
@media (max-width: 900px) {
	body {
		width: unset;
	}
}
</style>
