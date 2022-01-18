<template>
	<div>
		<div v-if="showMenus">
			<div class="content">
				<span class="material-icons" @click="showMenus = !showMenus">close</span>
				<p
					@click="
						hideChecks = !hideChecks;
						$emit('hideDone', hideChecks);
					"
				>
					Hide or show done todos <img src="../assets/visibility.svg" alt="eye" />
				</p>
				<p @click="$emit('deleteDone')">
					Delete done todos
					<img src="../assets/delete.svg" alt="eye" />
				</p>
				<p @click="$emit('clearData')">
					Clear all data
					<img src="../assets/delete_forever.svg" alt="eye" />
				</p>
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
			hideChecks: false,
			showMenus: false,
			showMenu: false,
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
	left: 0;
	height: 100vh;
	width: 100vw;
	background: rgba(128, 128, 128, 0.486);
}
span.material-icons {
	cursor: pointer;
	user-select: none;
	margin: 3% 0 0 95%;
	font-size: 2rem;
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
	p {
		user-select: none;
		cursor: pointer;
		display: flex;
		font-size: 1.3rem;
		background: rgba(70, 44, 64, 0.233);
		margin: 2rem 0;
		padding: 1rem;
		img {
			margin: 0 1rem 0 auto;
		}
		&:hover {
			background: rgba(70, 44, 64, 0.596);
		}
	}
	p:nth-child(4){
		margin-top: 45rem;
	}
	span{
		margin: 5% 0 0 85%;
	}
}
</style>
