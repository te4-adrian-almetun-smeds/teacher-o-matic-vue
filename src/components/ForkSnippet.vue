<template>
  <div class="codesnippet">
    <pre>
      <code :class="classes">
        {{snippet}}
      </code>
    </pre>
  </div>
</template>

<script lang="ts">
// eslint-disable-next-line @typescript-eslint/no-var-requires
const hljs = require("../../node_modules/highlight.js")
export default {
  name: "ForkSnippet",
  props: ["snippet", "classes"],
  mounted() {
    console.log(this)
    // Given that the call to this.$el works this should initialize code highlighting
    // hljs.highlightBlock(this.$el);
  }
}
</script>