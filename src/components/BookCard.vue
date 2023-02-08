<template>
  <div class="card" :class="item.favorite ? 'favorite' : ''">
    <p class="title">
      {{ item.title }}
    </p>
    <p class="price">
      {{ item.price }}
    </p>
    <p class="isbn">
      {{ item.isbn }}
    </p>
    <FavoriteButton @changeFavorite="handleFavorite(item)" />
  </div>
</template>

<script>
import FavoriteButton from "@/components/FavoriteButton.vue";
export default {
  components: {
    FavoriteButton,
  },
  props: {
    item: {
      type: Object,
    },
  },
  methods: {
    handleFavorite(book) {
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];

      if (book.favorite === undefined) {
        book.favorite = false;
      }

      book.favorite = !book.favorite;

      if (book.favorite) {
        favorites.push(book.isbn);
      } else {
        favorites.splice(favorites.indexOf(book.isbn), 1);
      }

      localStorage.setItem("favorites", JSON.stringify(favorites));
    },
  },
};
</script>
<style scoped>
.card {
  max-width: 400px;
  border: 2px solid lightgray;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.favorite {
  border-color: red;
}

.title {
  grid-column: span 3;
}
</style>
