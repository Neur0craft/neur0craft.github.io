<template>
  <div class="app">
    <aside class="sidebar">
      <nav class="sidebar-title">
        <RouterLink to="/">
          <h1 class="title">Neurøcraft</h1>
        </RouterLink>
        <h4>Blog</h4>
      </nav>
      <hr />
      <h3>Recent Posts</h3>
      <nav>
        <div v-for="post in recentPosts" :key="post.id">
          <router-link :to="`${post.destination}`">
            {{ post.title }}
          </router-link>
        </div>
      </nav>
    </aside>
    <main>
      <router-view class="content" />
      <FooterComponent />
    </main>
  </div>
</template>

<script setup lang="ts">
import FooterComponent from "./components/FooterComponent.vue";
</script>
