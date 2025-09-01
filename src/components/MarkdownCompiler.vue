<template>
  <div class="markdown-compiler" v-html="compiledHtml"></div>
</template>

<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import { marked } from "marked";
import { getHighlighter, codeToHtml } from "shiki";

const props = defineProps<{
  content: string;
}>();

const compiledHtml = ref("");
const shikiHighlighter = ref<any>(null);

// Configure marked with custom renderer for code blocks
const configureMarked = async () => {
  if (!shikiHighlighter.value) {
    shikiHighlighter.value = await getHighlighter({
      themes: ["github-dark"],
      langs: [
        "javascript",
        "typescript",
        "html",
        "css",
        "vue",
        "bash",
        "json",
        "markdown",
        "r",
      ],
    });
  }

  const renderer = new marked.Renderer();

  renderer.code = (code: string, language: string | undefined) => {
    if (!language || !shikiHighlighter.value) {
      return `<pre><code>${escapeHtml(code)}</code></pre>`;
    }

    try {
      const highlighted = codeToHtml(code, {
        lang: language,
        theme: "poimandres",
      });
      console.log(highlighted);
      return highlighted;
    } catch (error) {
      console.warn(
        `Failed to highlight code with language ${language}:`,
        error,
      );
      return `<pre><code>${escapeHtml(code)}</code></pre>`;
    }
  };

  marked.setOptions({
    renderer,
    breaks: true,
    gfm: true,
  });
};

// Helper function to escape HTML
const escapeHtml = (text: string): string => {
  console.log(text);
  const div = document.createElement("div");
  div.textContent = text;
  return div.innerHTML;
};

// Compile markdown to HTML
const compileMarkdown = async () => {
  await configureMarked();
  compiledHtml.value = marked.parse(props.content) as string;
};

// Watch for content changes
watch(() => props.content, compileMarkdown, { immediate: true });

// Initialize highlighter on component mount
onMounted(async () => {
  await configureMarked();
  compileMarkdown();
});
</script>

<style scoped></style>
