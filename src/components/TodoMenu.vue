<template>
	<div>
		<div v-if="showMenus"> 
			<div class="content">
				<button @click="showMenus = !showMenus">X</button>
				<p @click="$emit('hideDone'); hideOrShow = true">Hide done todos</p>
				<p @click="$emit('showDone'); hideOrShow = false" >show done todos</p>
				<p @click="$emit('deleteDone')">Delete done todos</p>
				<p @click="$emit('clearData')">Clear all data</p>
			</div>
			<div class="fade-layer"></div>
		</div>
		<span class="material-icons" @click="showMenus = !showMenus"> menu </span>
	</div>
</template>

<script>
export default {
	data() {
		return {
			showMenus: false,
			showMenu: false,
			hideOrShow: false
		};
	},
	// methods: {
	// 	hideDone(){
	// 		console.log(this.todoItems.filter(x => x == false))
	// 	}
	// },
	// props: {
	// 	todoItems: Array
	// },
};
</script>

<style lang="scss" scoped>
.fade-layer {
	position: fixed;
	height: 100vh;
	width: 100vw;
	background: rgba(128, 128, 128, 0.486);
}
span.material-icons {
	cursor: pointer;
	user-select: none;
	&:hover {
		color: grey;
	}
}
.content {
	z-index: 1;
	position: absolute;
	width: 20rem;
	background: whitesmoke;
	right: 0;
	height: 100vh;
}
</style>
