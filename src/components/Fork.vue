<template>
  <main class="fork" v-if="manifest">
    <h1>{{ fork.full_name }}</h1>
    <ForkSnippet :snippet="snippet" :classes="manifest.language"/>
    <a :href="fork.html_url">Show on github</a>
    <div class="comments">
      <p>test comment</p>
      <p>test comment</p>
      <p>test comment</p>
    </div>
  </main>
</template>

<script lang="ts">
import { ref } from "vue";
import ForkSnippet from "./ForkSnippet.vue";

export default {
  name: "Fork",
  props: ["fork"],
  components: { ForkSnippet },
  setup(props: any) {
    const isLoadingManifest = ref(false);
    const snippet = ref('');
    const getSnippet = async (path: string) => {
      const response = await fetch(
        `https://raw.githubusercontent.com/${props.fork.full_name}/${props.fork.default_branch}/${path}`
      );
      snippet.value = await response.text();
    };

    const manifest = ref({ filePath: "" });
    const getManifest = async () => {
      isLoadingManifest.value = true;

      const response = await fetch(
        `https://raw.githubusercontent.com/${props.fork.full_name}/${props.fork.default_branch}/.manifest.json`
      );

      manifest.value = await response.json();
      isLoadingManifest.value = false;
      getSnippet(manifest.value.filePath);
    };
    getManifest();

    return {
      manifest,
      isLoadingManifest,
      snippet
    };
  }
};
</script>

<style lang="scss" scoped>
main.fork {
  width: 20em;
  height: 30em;
  background-color: whitesmoke;
  border: solid gray 2px;
  margin: 2vw;
}
</style>
