<template>
  <div class="list">
    <h1>Articles</h1>
    <div class="container" v-if="this.kind === 'mostpopular'">
      <div v-for="article in info" class="article" :key="article.id">
        <div v-for="media in article.media" :key="media.caption">
          <div v-for="meta in media['media-metadata']" :key="meta.url">
            <img class="articleImage" v-bind:src="meta.url" v-if="meta.format == 'mediumThreeByTwo210'">
          </div>
        </div>
        <div class="articleText">
          <h2 class="articleHeader"><a v-bind:href="article.url" target="new">{{ article.title }}</a></h2>
        </div>
      </div>
    </div>
    <div class="container" v-else>
      <div v-for="article in info" class="article" :key="article.headline">
        <div v-for="media in article.multimedia" :key="media.src">
            <img class="articleImage" v-bind:src="media.src">
        </div>
        <div class="articleText">
          <div v-for="linkinfo in article.link" :key="linkinfo.url">
            <h2 class="articleHeader"><a v-bind:href="linkinfo.url" target="new">{{ article.headline }}</a></h2>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Content',
  data () {
    return {
      info:null,
    }
  },
  props: {
    periode: {
      type: String
    },
    kind: {
      type: String
    }
  },
  mounted () {
    axios
      .get('https://api.nytimes.com/svc/mostpopular/v2/emailed/1.json?api-key=j26bTLY9kAAokGwCxlHOHGcgXPi1SEDS')
      .then(response => (this.info = response.data.results))
  },
  watch: {
    periode: function() {
      if (this.kind == "mostpopular"){
        axios
          .get('https://api.nytimes.com/svc/' + this.kind + '/v2/emailed/' + this.periode + '.json?api-key=j26bTLY9kAAokGwCxlHOHGcgXPi1SEDS')
          .then(response => (this.info = response.data.results))
      }else{
        axios
          .get('https://api.nytimes.com/svc/' + this.kind + '/v2/reviews/all.json?api-key=j26bTLY9kAAokGwCxlHOHGcgXPi1SEDS')
          .then(response => (this.info = response.data.results))
      }
    }
  }
}
</script>

<style scoped>
div{
  margin:0;
}
h1{
  margin:0;
  padding:0;
  display:inline-block;
  width: 100%;
  text-align:center;
}
a{
  color:white;
  text-decoration: none;
}
.list{
  display: flex;
  flex-wrap: wrap;
  justify-content:space-evenly
}
.container{
  width:100%;
  display:contents;
}
.article{
  margin:20px;
  width:400px;
  height:250px;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 0 5px 0 black;
}
.article:hover{
  box-shadow: 0 0 10px 0 black;
  
}
.articleImage{
  width:100%;
  height:100%;
  transition: all 0.5s ease;
}
.articleImage:hover{
  transform: scale(1.1);
  filter: blur(2px);
}
.articleHeader{
  display: inline-block;
}
.articleText{
  position: relative;
  bottom: 280px;
  padding:0 10px;
  color:white !important;
  background-color: #0000009e;
}
</style>