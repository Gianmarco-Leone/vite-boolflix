<script>
export default {
  props: {
    name: String,
    originalName: String,
    language: String,
    vote: String,
    pic: String,
  },
  computed: {
    toUpperCaseLanguage() {
      return this.language.toUpperCase();
    },
  },
};
</script>

<template>
  <li>
    <img :src="`http://image.tmdb.org/t/p/w300${pic}`" />
    <span> TITLE: {{ name }} </span>
    <hr />
    <span> ORIGINAL TITLE: {{ originalName }} </span>
    <hr />
    <span> LANGUAGE: ({{ language }})</span>
    <!-- SE LA BANDIERA NON E' QUELLA INGLESE -->
    <div v-if="language != 'en'">
      <img
        :src="`https://www.countryflagicons.com/FLAT/64/${toUpperCaseLanguage}.png`"
        :alt="`${language} flag`"
      />
    </div>
    <!-- SE LA BANDIERA E' QUELLA INGLESE -->
    <div v-else-if="(language = 'en')">
      <img
        src="https://www.countryflagicons.com/FLAT/64/GB.png"
        :alt="`${language} flag`"
      />
    </div>
    <hr />
    <span> VOTE: {{ vote }} </span>
  </li>
</template>

<style lang="scss" scoped>
// debug
li {
  width: 300px;
  border: 1px solid black;
  margin: 1rem;
}
</style>
