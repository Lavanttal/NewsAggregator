<template>
  <div>
    <h1>News Feed</h1>
    <p>Change source</p>
     <v-overflow-btn
            class="my-2"
            :items="source"
            label="Source"
            target="#dropdown-example"
          ></v-overflow-btn>
       <Article :articles="articles"></Article>
      </div>
    </template>
</template>
<script>
import axios from "axios";
import Article from '../components/Article';
export default {
  components: {
    Article
  },
  head () {
    return {
    title: 'News Aggregator',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { name: 'keywords', content: 'keyword 1, keyword 2'},
      { hid: 'description', name: 'description', content: 'A news aggregator'}
    ],
    }
  },
  data () {
    return {
      source: ['TechCrunch', 'Reuters', 'Headlines NL', 'Headlines US'],
      articles: [],
    } 
  },

  async created() {
    const config = {
      headers: {
        'Accept': 'application/json'
      }
    }

    try {
    const res = await axios.get('https://newsapi.org/v2/top-headlines?sources=cnn&apiKey=9ea1ab728d064e058f5615edc94bf515', config);
          this.articles = res.data.articles;
          console.log(this.articles);
    } catch (err) {
  console.log(err);
    }
  }
}
</script>