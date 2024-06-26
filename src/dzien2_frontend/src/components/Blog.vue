<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="fetchPosts" class="bg-blue-600 rounded-lg text-white p-4">Refresh</button>
        </div>
            <div class="grid mx-6 gap-4 my-4">
                <div v-for="(post, index) in posts" class="drop-shadow-xl bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ post }}</p>
                <button  class="bg-blue-600 rounded text-white p-4" @click="deletePost(index)">Delete</button>
            </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="newBlog" class="border-2 border-blue-600 p-4" type="text">
            <button @click="addPost" class="bg-blue-600 rounded-lg text-white p-4">Post</button>
        </div>
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
        async deletePost(index){
            await dzien2_backend.delete_post(index);
            await this.fetchPosts();
        },
        async fetchPosts() {
            this.posts = await dzien2_backend.view_posts();
        }
    },
    async mounted(){
        this.fetchPosts()
    }
}
</script>