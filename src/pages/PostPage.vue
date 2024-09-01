<template>
    <div class="container my-4 text-center">
        <AppPost :post="currentPost" />
        <div class="text-start my-4">
            <a href="/" class="btn btn-warning">Back to Home</a>
        </div>
    </div>
</template>

<script>
import AppPost from "../components/AppPost.vue";

export default {
    components: {
        AppPost
    },
    data() {
        return {
            currentPost: null
        };
    },
    mounted() {
        // Recupera il post da localStorage
        const savedPost = JSON.parse(localStorage.getItem('post'));
        if (savedPost) {
            this.currentPost = savedPost;
        } else {
            console.error("Errore: Nessun post trovato in localStorage.");
        }
    },
    unmounted() {
        // Rimozione post
        localStorage.removeItem('post');
    }
}
</script>
