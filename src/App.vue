<template>
	<div id="app">
		<span v-if="isLoading" class="loading">
			Загруууууузка
		</span>
		<post-list
			v-else-if="postList && postList.length"
			:post-list="postList"
		/>
		<span v-else>
			Нет писеееееем
		</span>
	</div>
</template>

<script>
import PostList from './components/PostList'

export default {
	name: 'App',
	components: {
		PostList
	},
	data () {
		return {
			postList: null,
			isLoading: false
		}
	},
	mounted () {
		this.getPosts()
	},
	methods: {
		async getPosts () {
			this.isLoading = true

			try {
				const posts = await fetch('https://jsonplaceholder.typicode.com/posts')

				this.postList = await posts.json()
			} catch(err) { 
				console.log(err)
			} finally {
				this.isLoading = false
			}
		}
	}
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.loading {
	font-size: 28px;

	&:after {
		content: '';
		position: absolute;
		margin-left: 4px;
		animation: loading 1.5s infinite linear;
	}
}

@keyframes loading {
	25% {
		content: '.'
	}

	50% {
		content: '..'
	}

	100% {
		content: '...'
	}
}
</style>
