<template>
  <a class="item-container" :href="url">
    <div class="item-img">
      <img :src="item.poster.url" alt="Постер" />
    </div>
    <div class="item-info">
      <p>
        <b>{{ item.name }}</b>
      </p>
      <span> Рейтинг IMDb: {{ item.rating.imdb }} </span>
      <br />
      <span>
        Год:
        {{ item.year }}
      </span>
    </div>
  </a>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  computed: {
    url() {
      return `https://www.kinopoisk.ru/${this.item.type == "movie"?"film":"series"}/${this.item.id}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.item-container {
  &:hover {
    background: #eee;
  }
  display: flex;
  align-items: center;
  height: 6rem;
  padding: 0 10px;
  min-width: 400px;
  // border: 1px solid #000;
  text-decoration: solid none;
  color: #000;
}
.item-img {
  width: 3.4rem;
  height: 4.8rem;
  img {
    border-radius: 0.2rem;
    width: 100%;
    height: 100%;
  }
}
.item-info {
  margin-left: 12px;
}
</style>