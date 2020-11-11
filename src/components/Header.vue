<template>
  <nav>
    <HeaderSearch
      placeholder="Enter Username"
      @changed="input => $emit('changed', input)"
    />
    <a
      href="https://github.com/login/oauth/authorize?client_id=potatoe"
      >Github</a
    >
  </nav>
</template>

<script lang="ts">
// import Vue from 'vue'
import HeaderSearch from "./HeaderSearch.vue";

export default {
  name: "Header",
  components: {
    HeaderSearch
  },
  // data() {

  // },

  methods: {
    // onChanged(input : string) {
    //   $emit('changed', input)
    // }
  }
}
</script>


<style lang="scss" scoped>
    nav{
        background-color: lightcoral;
        display: flex;
        justify-content: center;
        align-items: flex-start;
        // flex-wrap: wrap;
        
        padding: 2vh 2vw;
        height: 10vh;
        width: 100vw;

        a{
            width: fit-content;
            height: fit-content;
            padding: 1.5vh 4vw;
            background-color: whitesmoke;
            margin: auto 2.5vw auto 2.5vw;
            border-radius: 0.5vw;
            font-weight: 900;
            color: black;
            text-decoration: none;
        }
    }
</style>