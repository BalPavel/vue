<template>
  <div class="content">
    <h2>Тут представлено несколько реализаций работы с API</h2>
    <ol>
      <li>
        <b>Просто рандомный факт:</b>
        <br>
        Источник API: <a href="https://uselessfacts.jsph.pl">https://uselessfacts.jsph.pl</a>
        <h4>{{ randomFact }}</h4>
      </li>
      <li>
        <b>Факт о введённом числе:</b>
        <br>
        Источник API: <a href="http://numbersapi.com/">http://numbersapi.com/</a>
        <br>
        <form @submit.prevent="submitNumber">
          Случайное число:
          <input type="checkbox" v-model="isRandomNumber">
          <br>
          Выбор категории:
          <select v-model="selectedTypeFact">
            <option value="trivia">Trivia</option>
            <option value="math">Math</option>
            <option value="date">Date</option>
            <option value="year" v-if="isRandomNumber">Year</option>
          </select>
          <br>
          <input type="text"
            required
            v-model="numberForFact"
            v-if="!isRandomNumber"
            :placeholder="placeholderForSelected"
          />
          <button type="submit">Apply</button>
        </form>
        <h4>{{ numberFact }}</h4>
      </li>
      <li>
        <Kinopoisk />
      </li>
    </ol>
  </div>
</template>

<script>
import Axios from 'axios';
import Kinopoisk from '@/components/Kinopoisk.vue'
export default {
  data() {
    return {
      randomFact: '',
      numberFact: '',
      numberForFact: '',
      selectedTypeFact: 'trivia',
      isRandomNumber: false,
    }
  },
  components: {
    Kinopoisk,

  },
  methods: {
    submitNumber() {
      // console.log(this.numberForFact, this.selectedTypeFact);
      let url = "";
      if (this.isRandomNumber) {
        url = `http://numbersapi.com/random/${this.selectedTypeFact}`;
      } else {
        url = `http://numbersapi.com/${this.numberForFact}/${this.selectedTypeFact}`;
      }
      Axios.get(url)
      .then((response) => response.data)
      .then((fact) => {
        // console.log(fact);
        this.numberFact = fact;
      });
    }
  },
  watch: {
    selectedTypeFact() {
      this.numberForFact = "";
    }
  },
  computed: {
    placeholderForSelected() {
      switch (this.selectedTypeFact) {
        case "trivia":
          return "18"
        case "math":
          return "1"
        case "date":
          return "mm/dd"
      }
    }
  },
  mounted() {
    Axios.get("https://uselessfacts.jsph.pl/random.json?language=en")
      .then((response) => response.data)
      .then((json) => {
        // console.log(json.text);
        this.randomFact = json.text.trim();
        // this.loading = false;
      });
  },
}
</script>

<style lang="scss">
  .content {
    background: #eee;
    width: 50%;
    flex: 1 0 auto;
    // min-width: 400px;
    h2,h3,h4 {
      text-align: center;
    }
    ol {
      margin-bottom: 0px;
      li {
        background: #ddd;
        margin-right: 40px;
      }
    }
    h4 {
      margin-top: 3px;
    }
    select {
      margin-bottom: 3px;
    }
    input {
      margin-bottom: 3px;
      margin-right: 3px;
    }
  }
</style>