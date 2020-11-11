<template>
  <input
    :placeholder="placeholder"
    v-model="text"
    @keyup.enter="$emit('changed', text)"
  />
</template>

<script lang="ts">
export default {
  name: 'HeaderSearch',
  props: ['placeholder'],
  data(){
    return {
      text: ""
    }
  },
}
</script>

<style lang="scss" scoped>
input {
  width: 50vw;
  height: 4vh;
  background-color: whitesmoke;
  border: none;
  color: black;
  margin: auto 0 auto 0;
  padding-left: 1.5vw;
}

input::placeholder {
  color: gray;
}
</style>