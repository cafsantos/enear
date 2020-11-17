<template>
  <div>
    <h1 class="text-3xl mb-4">Kanye West quotes</h1>

    <div class="mb-5">
      <button
        @click="newQuote"
        class="border border-green-400 bg-green-400 text-white px-6 py-2 rounded hover:bg-green-500 mr-4"
      >
        Inspire me
      </button>

      <button
        @click="deleteAllQuotes()"
        class="border border-red-500 px-6 py-2 rounded hover:bg-red-100"
      >
        Delete All
      </button>
    </div>

    <div v-for="quote of quotes" v-bind:key="quote.id">
      <div class="my-2 text-lg flex">
        <button
          @click="deleteQuote(quote.id)"
          class="bg-red-400 text-white w-6 h-6 leading-none rounded-full flex items-center justify-center mr-3"
        >
          x
        </button>
        <p>“{{ quote.quote }}”</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "Quotes",

  data() {
    return {
      quotes: [],
    };
  },

  methods: {
    newQuote() {
      axios
        .get("https://api.kanye.rest/")
        .then(
          (response) =>
            (this.quotes = [
              ...this.quotes,
              { id: uuidv4(), quote: response.data.quote },
            ])
        );
    },
    deleteQuote(id) {
      this.quotes = this.quotes.filter((quote) => quote.id !== id);
    },
    deleteAllQuotes() {
      this.quotes = [];
    },
  },

  mounted() {},
};
</script>

<style>
</style>