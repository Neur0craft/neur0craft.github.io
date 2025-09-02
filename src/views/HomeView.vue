<template>
  <div class="home-view">
    <MarkdownCompiler :content="markdownContent" />
  </div>
</template>

<script setup lang="ts">
import MarkdownCompiler from "@/components/MarkdownCompiler.vue";

const markdownContent = `
# Welcome to Neurøcraft

> If you are interested in joining
 [Sign up ->](https://forms.office.com/Pages/ResponsePage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAN__kbEWuxUOVVUVUQ2RjhRS1lQRTk3SzRMNkNIV0tYWS4u)

<br/>

We engage in activities such as:
- Data Analysis
- Machine Learning
- Mathematical Modeling
- Prompt Engineering

If you possess qualities like curiosity, creativity, and passion, we invite you to join our community.

Contact us at: ericyan534@gmail.com

`;
</script>
