<template>
  <div>
    <b>Поиск фильмов и сериалов на кинопоиске:</b>
    <br />
    <form @submit.prevent="submitSearch">
      <input type="text" class="search" v-model="searchRequest" />
      <button type="submit">Поиск</button>
    </form>
    <div class="searchResults" v-show="showResults" id="searchResults">
      <Loader v-show="isLoading" />
      <div v-show="!isLoading">
        <ResultItem
          class="resultItem"
          v-for="item in this.searchResults"
          :key="item.id"
          :item="item"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
import ResultItem from "@/components/ResultItem.vue";
import Loader from "@/components/Loader.vue";

export default {
  components: {
    ResultItem,
    Loader,
  },
  data() {
    return {
      token: "E5QD90F-R5Y4AJ4-GDMQSFS-FQWT2Z5",
      searchRequest: "",
      showResults: false,
      searchResults: null,
      isLoading: false,
    };
  },
  methods: {
    dropdown(e) {
      let el = this.$refs.dropdown;
      // console.log(el);
      let target = e.target;
      // console.log(e);
      if (el !== target) {
        this.showResults = false;
      }
    },
    submitSearch() {
      // FIXME:Не работает отображение лоудера, но при ручной перестановке true/false в браузере всё работатет.
      // Думаю, проблема в этой функции
      if (this.searchRequest.trim()) {
        this.showResults = true;
        this.isLoading = true;

        let url =
          `https://api.kinopoisk.dev/movie?` +
          `search=${encodeURI(this.searchRequest)}` +
          `&field=name` +
          `&isStrict=false` +
          `&token=${this.token}`;
        console.log(url);
        Axios.get(url).then((result) => {
          this.searchResults = result.data.docs;
        });

        this.isLoading = false;

      } else {
        this.searchRequest = "";
      }
    },
  },
  watch: {
    searchRequest() {
      this.showResults = false;
      this.searchResults = undefined;
    },
  },
  created() {
    document.addEventListener("click", this.dropdown);
  },
  destroyed() {
    document.removeEventListener("click", this.dropdown);
  },
};
</script>

<style lang="scss" scoped>
.searchResults {
  position: absolute;
  background: #fff;
  display: flex;
  flex-direction: column;
  border-radius: 0.3rem;
  border: 1px solid #ccc;
  max-height: 300px;
  overflow: auto;
}
</style>
