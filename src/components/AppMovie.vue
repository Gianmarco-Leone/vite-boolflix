<script>
export default {
  props: {
    title: String,
    originalTitle: String,
    language: String,
    vote: String,
  },
};
</script>

<template>
  <li>
    <span> TITLE: {{ title }} </span>
    <br />
    <span> ORIGINAL TITLE: {{ originalTitle }} </span>
    <br />
    <span> LANGUAGE: {{ language }} </span>
    <br />
    <span> VOTE: {{ vote }} </span>
  </li>
</template>

<style lang="scss" scoped>
// debug
li {
  width: 300px;
  border: 1px solid black;
}
</style>
