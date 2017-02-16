<template>
    <div class="newslist card-columns">
        <div class="card" v-for="article in articles">
            <a v-bind:href="article.url" target="_blank"><img class="card-img-top img-fluid" v-bind:src="article.urlToImage"/></a>
            <div class="card-block">
                <h5 class="card-title"><a v-bind:href="article.url" target="_blank">{{article.title}}</a></h5>
                <p class="card-text">{{article.description}}</p>
            </div>
            <div class="card-footer">
                <small class="text-muted">Last updated {{ article.publishedAt | moment("from") }}.</small>
                <small class="text-muted">By {{ article.author }}.</small>
            </div>
        </div>
</template>

<script>
    export default {
        name: 'newslist',
        props: ['source'],
        data () {
            return {
                articles: []
            }
        },
        methods: {
            updateSource: function (source) {
                this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=f4619b589f6e4134a73b1029f972329b')
                .then(response => {
                    this.articles = response.data.articles;
                });
            }
        },
        created: function (){
            this.updateSource('bbc-news');
        },
        watch: {
            source: function (val){
                this.updateSource(val);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .card{
        padding: 0;
        background: #f9f9f9;
        border-radius: 0;
    }
</style>