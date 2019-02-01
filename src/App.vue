<template lang="pug">
  div#app
    h1.f1 ⭐ Quote Maker v0.1 ⭐
    button(v-on:click="getNewQuote()") Generate quote
    blockquote#quote "{{ quote.saying }}"
    label(for="quote") - {{ quote.author }}
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      quote: {
        saying: 'It\'s not my fault',
        author: 'Han Solo'
      }
    }
  },
  methods: {
    getNewQuote() {
      axios({
        method: 'get',
        url: 'http://quotesondesign.com/wp-json/posts?filter[orderby]=rand&filter[posts_per_page]=1'
      })
      .then(response => {
        this.quote.saying = response.data.quote
        this.quote.author = response.data.author
      })
    }
  }
}
</script>

<style lang="scss">
  #app {
    // font-size: 14px;
    position: relative;
    width: 75%;
    margin: 2rem auto;
    font-family: 'niramit', serif;
  }
  h1 {
    font-weight: 100;
    font-size: 1.3rem;
    text-align: center;
  }
  blockquote {
    font-family: 'niramit', serif;
    width: auto;
    margin: 4rem auto 3rem auto;
    text-align: left;
    display: block;
    font-size: 35px;
  }
  label {
    font-family: 'roboto', serif;
    display: block;
    position: absolute;
    right: 10;
    font-size: 20px;
  }
  button {
    font-family: 'Roboto', sans-serif;
    display: block;
    margin: 3rem auto;
    width: auto;
    background-color: lavender;
    border: none;
    font-size: 15px;
    padding: 12px 15px;
    border-radius: 5px;
    box-shadow: 0 20px 15px -10px rgba(0, 0, 0, 0.3);
    transition: .3s all ease-in-out;
    &:active {
      bottom: 200;
      transform: scale(0.95);
    }
  }
</style>
