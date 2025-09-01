<template>
  <div class="home-view">
    <MarkdownCompiler :content="markdownContent" />
  </div>
</template>

<script setup lang="ts">
import MarkdownCompiler from "@/components/MarkdownCompiler.vue";

const markdownContent = `
# Welcome to Neurøcraft
We engage in activities such as:
- Data Analysis
- Machine Learning
- Mathematical Modeling
- Prompt Engineering

If you possess qualities like curiosity, creativity, and passion, we invite you to join our community.

Contact us at: ericyan534@gmail.com

`;
</script>
