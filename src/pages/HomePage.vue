<template>
  <div class="text-center">
    <h1 class="my-4">{{ titlePost }}</h1>
    <ul>
      <li v-for="(post, i) in store.posts" :key="i" class="py-2">
        <a
          href="#"
          :class="{ 'text-muted': isClicked(post.day) }"
          @click.stop="handlePostClick(i)"
        >
          <span class="h6">Giorno {{ post.day }}:</span> {{ post.title }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import importPosts from "../assets/posts.json";
import { store } from "../store";

export default {
  data() {
    return {
      store,
      titlePost: importPosts.tripTitle,
      clickedLinks: JSON.parse(localStorage.getItem("clickedLinks")) || [],
    };
  },
  methods: {
    takeAllPost() {
      if (this.store.posts.length == 0) {
        for (let i = 0; i < importPosts.days.length; i++) {
          const post = importPosts.days[i];
          this.store.posts.push(post);
        }
      }
    },
    takePostDay(i) {
      const selectedPost = this.store.posts[i];
      if (selectedPost) {
        localStorage.setItem("post", JSON.stringify(selectedPost));
        this.clickedLinks.push(selectedPost.day);
        localStorage.setItem("clickedLinks", JSON.stringify(this.clickedLinks));
      } else {
        console.error("Errore: Post non trovato all'indice", i);
      }
    },
    handlePostClick(i) {
      this.takePostDay(i);

      // Timer
      setTimeout(() => {
        this.$router.push(`/${this.store.posts[i].day}`);
      }, 500);
    },
    isClicked(day) {
      // Controlla se il giorno è già presente nell'array dei link cliccati
      return this.clickedLinks.includes(day);
    },
  },
  mounted() {
    this.takeAllPost();
  },
};
</script>

<style lang="scss" scoped></style>
