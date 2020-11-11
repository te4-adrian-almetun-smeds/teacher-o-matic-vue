<template>
  <main>
    <h1>{{ repo.name }}</h1>
    <div class="parentBox">
      <div class="forks" @click="$emit('showforks', repo.full_name)">
        Show forks
      </div>
      <p class="divider">|</p>
      <a :href="repo.html_url" class="github">Show on Github</a>
    </div>
    <p>{{ repo.forks }}</p>
  </main>
</template>

<script lang="ts">
export default {
  name: "Repo",
  props: ["repo"]
}
</script>


<style lang="scss" scoped>
main {
  font-family: "Josefin Sans", sans-serif;
  width: 40vw;
  height: 10vh;
  margin: 2.5vw;
  background-color: whitesmoke;
  border: solid 2px lightgray;
  display: grid;
  grid-template-rows: 50% 50%;
  grid-template-columns: 75% 25%;
  grid-template-areas:
    "name ."
    "box counter";
  h1 {
    font-size: 3vw;
    margin: 1vh;
    grid-area: name;
  }

  .parentBox {
    grid-area: box;
    width: fit-content;
    height: fit-content;
    margin-top: auto;
    display: flex;
    justify-content: center;
    align-items: center;

    a,
    .forks {
      text-decoration: none;
      color: rgb(106, 106, 255);
      text-align: center;
    }

    a{
      margin: 0 0 0 5%;
    }

    .forks {
      margin: 0 5% 0 0;
      cursor: pointer; 
    }
  }

  p:not(.divider) {
    grid-area: counter;
    width: fit-content;
    height: fit-content;
    margin: auto 15% 15% auto;
  }
}
</style>
