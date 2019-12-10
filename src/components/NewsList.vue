<template>
    <div>
        <div class="container">
            <div class="media" v-for="article in articles" :key="article.id">
                <div class="media-left media-middle">
                   <a :href="article.url" target="_blank"><img :src="article.urlToImage" class="media-object"></a>
                </div>
                <div class="media-body">
                    <h4 class="media-heading"><a :href="article.url" target="_blank">{{article.title}}</a></h4>
                    <p>{{article.description}}</p>
                    <p><i>{{article.author}}</i></p>
                </div>
            </div>
        </div>
    </div>
</template>


<script>

export default {
    name: 'NewsList',
    props:{
        source: ""
    },
    methods: {
         updateSource: function(source) {
             this.$http.get('https://newsapi.org/v2/everything?sources='+ source + '&language=en&pageSize=50&apiKey=cf0866b5aaef42e995f9db37bb3f7ef4')
             .then(response => {
                 this.articles = response.data.articles;
             })
             .catch(error => console.log(error));
         }
    },
    watch:{
        source : function(val) {
            this.updateSource(val);
        }
    },
    data () {
        return {
            articles: []
        }
    },
    created () {
      this.updateSource(this.source); 
    }
}
</script>



<style scoped>
.media-object {
    width: 120px;
    padding: 10px;
}
.media {
    border-top: 1px solid lightgray;
    padding-top: 20px;
}
</style>