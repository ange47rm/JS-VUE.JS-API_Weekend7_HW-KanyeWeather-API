<template>
<div id='kanyequotes'>
  <h2>Kanye Epic Quotes 4 U</h2>
  <h3> {{ quote }} </h3>
  <img src='https://i.pinimg.com/originals/16/92/71/169271f2d449fb9203707bdbcee9ffdf.jpg' width="300">
  <br>
  <button v-on:click='newKanyeQuote'>MORE KANYE WISDOM PLS</button>
</div>
</template>

<script>
export default {
    name: 'kanye-quote',
    props: ['quote'],
    methods: {
        newKanyeQuote(){
            fetch ("https://api.kanye.rest/")
            .then (response => response.json())
            .then (kanyeQuote => this.quote = kanyeQuote.quote)
        }
    }
}
</script>

<style>

#kanyequotes {
    border: 5px solid rgb(0, 255, 55);
    padding: 10px;
    text-align: center;
    background-color: white;
    margin: 50px;
}

</style>