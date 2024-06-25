<template>
    <div>
        <button @click="fetchPosts">Refresh</button>
        Hello
        {{ posts }}
        <input v-model="newBlog" type="text">
        <button @click="addPost">Post</button>
    </div>
</template>


<script>
import {dzien2_backend} from 'declarations/dzien2_backend/index';

export default {
    data(){
        return {
            posts: [],
            newBlog: ""
        }
    },
    methods: {
        async addPost() {
            await dzien2_backend.add_post(this.newBlog);
        },
        async fetchPosts() {
            this.posts = await dzien2_backend.view_posts();
        }
    },
}
</script>