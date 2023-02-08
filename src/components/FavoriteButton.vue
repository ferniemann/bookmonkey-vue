<template>
  <button @click="favoriteState">Favorite</button>
</template>

<script>
export default {
  methods: {
    favoriteState() {
      this.$emit("changeFavorite");
    },
  },
};
</script>

<style lang="scss" scoped></style>
