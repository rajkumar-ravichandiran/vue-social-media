<template>
	<div class="feed" @scroll="handleScroll">
		<div v-for="post in posts" :key="post.id" class="post">
			<div class="post-header">
				<img :src="getUserAvatar(post.userId)" alt="User Avatar" class="avatar"/>
				<div>
					<p class="username">{{ getUserName(post.userId) }}</p>
				</div>
			</div>			
			<p class="post-title">{{ post.title }}</p>
			<p class="post-body">{{ post.body }}</p>
			
			<button v-if="!comments[post.id]" @click="fetchComments(post.id)">View Comments</button>
	
			<div v-if="comments[post.id] && comments[post.id].length > 0" class="comments">
				<div v-for="comment in comments[post.id].slice(0, displayedComments[post.id] || 2)" :key="comment.id" class="comment">
					<div class="comment-header">
						<p class="comment-author">{{ comment.name }}</p>
						<p class="comment-email">{{ comment.email }}</p>
					</div>
					<p class="comment-body">{{ comment.body }}</p>
				</div>
				<button v-if="comments[post.id] && displayedComments[post.id] < comments[post.id].length" @click="displayedComments[post.id] += 3">Load More Comments</button>
			</div>
		</div>
	
		<div v-if="loadingPosts" class="loading">Loading...</div>
	</div>
</template>
	
<script>
	import axios from "axios";
	
	export default {
		data() {
			return {
				posts: [],
				comments: {},
				displayedComments: {},
				userNames: {
					1: "Aravind Kumar",
					2: "Priya Subramanian",
					3: "Rajeshwari Natarajan",
					4: "Karthik Ram",
					5: "Anjali Venkatesan",
					6: "Santhosh Reddy",
					7: "Divya Krishnan",
					8: "Hariharan Rajagopal",
					9: "Shalini Srinivasan",
					10: "Ravi Chandran"
				},
				postPage: 1,
				loadingPosts: false,
				postsPerPage: 10,
				hasMorePosts: true,
			};
		},
		methods: {
			async fetchPosts() {
				if (!this.hasMorePosts) return;
				try {
					this.loadingPosts = true;
					const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${this.postPage}&_limit=${this.postsPerPage}`);
					if (response.data.length === 0) {
						this.hasMorePosts = false;
					} else {
						this.posts = [...this.posts, ...response.data];
						this.postPage += 1;
					}
					this.loadingPosts = false;
				} catch (error) {
					console.error("Error fetching posts:", error);
				}
			},
			async fetchComments(postId) {				
				try {
					const response = await axios.get(`https://jsonplaceholder.typicode.com/comments?postId=${postId}`);
					if (!this.comments[postId]) {
						this.comments[postId] = [];
					}
					this.displayedComments[postId] = 3;		
					this.comments[postId] = [...this.comments[postId], ...response.data];
				} catch (error) {
					console.error("Error fetching comments:", error);
				}
			},		
			handleScroll(event) {
				const threshold = 10;
				const target = event.target;
				const isAtBottom = target.scrollHeight - target.scrollTop - target.clientHeight <= threshold;
				if (isAtBottom && !this.loadingPosts) {
					this.fetchPosts();
				}
			},		
			getUserName(userId) {
				return this.userNames[userId] || "Unknown User";
			},		
			getUserAvatar(userId) {
				return `https://picsum.photos/50?random=${userId}`;
			}
		},
		mounted() {
			this.fetchPosts();
		}
	};
</script>	