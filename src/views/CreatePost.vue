<template>
	<div class="createPost">
		<h1>Postez un article!</h1>
		<div class="postInputDiv">
			<input type="text" id="titre" placeholder="Titre..." v-model="post.title">
		</div>
		<div class="postInputDiv">
			<textarea id="post" placeholder="Post..." v-model="post.post"></textarea>
		</div>
		<button id='postBtn' @click="createPost">PUBLIER</button>
	</div>
</template>


<script>
import axios from 'axios'

export default {
	name: 'CreatePost',
	data() {
		return {
			post: {
				title: null,
				post: null,
				userId: this.$store.state.auth.user.userId,
			}
		}
	},
	methods: {
		createPost(e) {
			axios.post("http://localhost:3000/api/posts", this.post)
			.then((result) => {
				console.log(result)
				alert('Post successfully created!');
			})
			.then(() => this.$router.push("/"))
			e.preventDefault();
		}
	} 
}
</script>


<style lang="scss">
@import '@/assets/main.scss';

.postInputDiv{
	margin: 1em;
	#titre{
		width: 60vw;
	}
	#post{
		width: 60vw;
		height: 40vh;
	}
}
#postBtn{
	margin: 0.3em;
	@include blueButton;
}
</style>
