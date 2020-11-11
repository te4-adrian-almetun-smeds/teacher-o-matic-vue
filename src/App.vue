<template>
  <Header @changed="fetchRepos" />
  <main class="wrapper" v-if="!this.displayForks" >
    <div class="cont" v-if="!displayContent" >
      <Welcome />
    </div>
    <div class="cont" v-else>
      <Repo
        v-for="repo in repos"
        :key="repo"
        :repo="repo"
        @showforks="fetchForks"
      />
    </div>
  </main>

  <main class="wrapper" v-if="this.displayForks">
    <Fork v-for="fork in forks" :key="fork.full_name" :fork="fork" />
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Header from "./components/Header.vue";
import Repo from "./components/Repo.vue";
import Welcome from "./components/Welcome.vue";
import Fork from "./components/Fork.vue";

export default defineComponent({
  name: "App",
  data() {
    return {
      displayContent: false,
      displayForks: false,
      repos: [],
      forks: []
    }
  },

  methods: {
    async fetchRepos(inputText: string) {
      const request = await fetch(
        `http://localhost:9295/api/github/${inputText}/repos`
      );
      const answer = await request.json();
      console.log(answer);
      this.repos = answer;
      this.displayContent = true;
    },

    async fetchForks(fullName: string) {
      const request = await fetch(
        `http://localhost:9295/api/github/${fullName}/forks`
      );
      const answer = await request.json();
      console.log(answer);
      this.forks = answer;
      this.displayForks = true;
    }
  },
  components: {
    Header,
    Repo,
    Welcome,
    Fork
  }
});
</script>

<style lang="scss">
.wrapper .cont{
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
body {
  margin: 0;
}

main.wrapper{
  width: 100vw;
  height: fit-content;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
</style>
