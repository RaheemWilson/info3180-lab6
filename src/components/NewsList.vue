<template>
    <ul class="news__list">
        <li v-for="article in articles" class="news__item">
            <img :src="article.urlToImage" :alt="article.title" />
            <div class="news__content">
                <p class="news__title">{{ article.title }}</p>
                <p>{{  article.description }}</p>
            </div>
        </li>
    </ul>
</template>
<script>
export default {
    data() {
        return {
            articles: []
        };
    },

    created() {
        let self = this;
        fetch(`https://newsapi.org/v2/top-headlines?country=us&apiKey=${import.meta.env.VITE_NEWSAPI_TOKEN}`,
        {
            headers: {
                'Authorization':`Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
        }).then(function(response) {
            return response.json();
        }).then(function(data) {
            console.log(data);
            self.articles = data.articles;
        });
    }
}
</script>

<style scoped>
    .news__list{
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 1rem;
        list-style-type: none;
    }

    .news__item{
        border: 1px solid #cccccc;
        border-bottom: 6px solid #14b8a7;
        border-radius: 6px;
    }

    .news__content{
        padding: 1rem;
    }

    .news__item img{
        height: 150px;
        width: 100%;
        border-radius: 6px 6px 0 0;
    }

    
</style>