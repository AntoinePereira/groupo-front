<template>
	<div class = 'usersList'>
		<div class="userTag" v-for="user in users" :key="user.id">
			<router-link :to="`/user/${user.id}`">
				<h1>{{ user.prenom }} {{ user.nom }}</h1>
				<h2 v-if="user.isAdmin  === 1">Admin</h2>
			</router-link>
		</div>
	</div>
</template>


<script >
	import { mapState } from "vuex"
	export default {
		computed: {
			...mapState('users', ['users'])
		},
		mounted() {
			this.$store.dispatch('users/loadUsers')
		},
	}
</script>


<style scoped lang="scss">
@import '@/assets/main.scss';

.usersList{
	@include wrapper;
	align-items: stretch;
	
}
.userTag{
	@include card;
	margin: 1em;
	overflow: hidden; 
	a{
		text-decoration: none;
		color: $color-secondary;
	}
}
</style>
