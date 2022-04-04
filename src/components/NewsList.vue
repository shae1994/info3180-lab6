<template>
    <form  @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm"
                id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
    <p>You are searching for {{ searchTerm }}</p>
    </form>

    <ul class="news__list">
    <li v-for="article in articles"
    class="news__item">
        <div  class="img-responsive"><img id="images" :src= article.urlToImage /></div>
        <div class="text-styler">{{ article.title }}</div>
        <div class="desc">{{ article.description }}</div>
        </li>
        
        </ul>
    
    
</template>


<script>
    export default {
        data() {
            return {
                articles:[],
                searchTerm: ''
            };
        },
        created() {
            let self = this;
            fetch('https://newsapi.org/v2/top-headlines?country=us',
            {
            headers: {
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
            })
            .then(function(response) {
                return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles=data.articles;
            });
        },
        methods: {
            searchNews() {
                    let self = this;
                    fetch('https://newsapi.org/v2/everything?q='+self.searchTerm + '&language=en', {
                        headers: {'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,}
                    })
                    .then(function(response) {
                        return response.json();
                    })
                    .then(function(data) {
                        console.log(data);
                        self.articles = data.articles;
                    });
                }
            }
    }
</script>

<style>


.news__list{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows:auto;
    grid-gap: 10px;
    padding-top: 5%;
    margin: 0px;
    
    
}
.news__item{
    border: 2px solid rgba(235, 235, 235, 0.64);
    border-bottom: 6px solid green;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius:10px;
    }


#images{
    width:295px;
    height: 200px;
}

p{
    text-align: center;
}

ul{
    list-style: none;
}

.text-styler{
    padding: 7px;
    font-weight: bold;
    text-align: left;
    inline-size: 295px;
    overflow-wrap: break-word;
}

.desc{
    text-align: left;
    padding-bottom: 10%;
    padding-left: 7px;
    padding-right: 7px;
    inline-size: 295px;
    overflow-wrap: break-word;
}


</style>