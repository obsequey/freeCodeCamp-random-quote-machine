<template lang="pug">
  div.flex.flex-column.items-center
    h1.f1.pv4 Quote Maker v0.1
    blockquote#quote.h4.f3.pv3.ph5.lh-title {{ quote.saying }}
    label(for="quote").h3.f4.pv3 - {{ quote.author }}
    button(v-on:click="getNewQuote()").w5.h2.mv3.pointer.shadow-4 Generate quote
    a(href="https://breaking-bad-quotes.herokuapp.com").f7.link.black.hover-gray More quotes ~
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
      // axios({
      //   method: 'get',
      //   url: 'https://breaking-bad-quotes.herokuapp.com/v1/quotes'
      // })
      // .then(response => {
      //   this.quote.saying = response.data[0].quote
      //   this.quote.author = response.data[0].author
      // })
      let request = new XMLHttpRequest();

      request.open('GET', 'https://breaking-bad-quotes.herokuapp.com/v1/quotes', true)

      request.onload = () => {
        let data = JSON.parse(request.response)

        this.quote.saying = data[0].quote
        this.quote.author = data[0].author
      }

      request.send()
    }
  }
}
</script>
