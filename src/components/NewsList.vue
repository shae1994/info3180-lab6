<template>

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
    return { articles:[]};
    },
    created() {
        let self = this;

        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
        Authorization: `Bearer  ${import.meta.env.VITE_NEWSAPI_TOKEN}`
        }
        })
    .then(function(response) {
    return response.json();
    })
    .then(function(data) {
    console.log(data);
    self.articles = data.articles;
    });
    }
    };
</script>

<style>
.news__list{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto;
    grid-gap: 20px;
    text-allign: justify;
    padding-top: 5%;
    padding-bottom: 10%;
    
    
}
.news__item{
    border: 2px solid rgba(235, 235, 235, 0.64);
    border-bottom: 6px solid green;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius:10px;
    }


#images{
    width:100%;
    height: 35vh;
}

ul{
    list-style: none;
}

.text-styler{
    padding: 7px;
    font-weight: bold;
    text-align: left;
}

.desc{
    padding: 10px 10px;
    text-align: left;
}


</style>