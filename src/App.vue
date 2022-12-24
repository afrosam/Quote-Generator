<template>
    <div class="container">
      <div class="quoteBox show">
        <h1><i class="fa fa-quote-left"></i> {{ quote }}</h1>
        <h3><i>{{ author }}</i></h3>
      </div>
      <div class="btnBar">
        <div class="social">
          <a class="btn primary-bg" :href="`https://twitter.com/intent/tweet?hashtags=quotes&related=freecodecamp&text=${quote}${author}`"><i class="fa fa-twitter" aria-hidden="true"></i></a>
          <a class="btn primary-bg" :href="`https://www.tumblr.com/widgets/share/tool?posttype=quote&tags=quotes,freecodecamp&caption=${author.slice(2)}&content=${quote}&canonicalUrl=https%3A%2F%2Fwww.tumblr.com%2Fbuttons&shareSource=tumblr_share_button`"><i class="fa fa-tumblr" aria-hidden="true"></i></a>
        </div>
        <a class="bigBtn primary-bg" href="" @click.prevent="getQuote"><span>New quote</span></a>
      </div>
    </div>
</template>

<script>
import Qs from './assets/quotes.json';

export default {
  name: 'App',
  data() {
    return {
      quotes: Qs,
      quote: '',
      author: ''
    }
  },
  methods: {
    getQuote() {
      let filteredQs = this.quotes.filter(quote => quote.author != this.author);
      let index = Math.floor(Math.random() * filteredQs.length);
      let fullQuote = {...filteredQs[index]};
      this.changeColor();
      setTimeout(() => {
        this.quote = fullQuote.quote;
        this.author = fullQuote.author;
      }, 500);
    },
    changeColor() {
      let quoteBox = document.querySelector('.quoteBox');
      quoteBox.classList.remove('show');
      quoteBox.classList.add('hide');
      let nodes = document.querySelectorAll('.primary-bg');
      let color = Math.floor(Math.random() * 360);
      let container = document.querySelector('.container');
      container.style.color = `hsl(${color}, 50%, 40%)`;
      nodes[0].addEventListener('transitionend', () => {
        quoteBox.classList.remove('hide');
        quoteBox.classList.add('show');
      });
      nodes.forEach((ele) => {
        ele.style.backgroundColor = `hsl(${color}, 50%, 40%)`
      });
      
    }
  },
  mounted() {
    this.getQuote()
  }
}
</script>
