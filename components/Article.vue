// HTML CONTENT
<template>
  <article ref="article">
    <h2>{{ article.title }}</h2>
    <p>{{ article.content }}</p>
  </article>
</template>


// TYPESCRIPT CONTENT
<script lang="ts">

// libs
import { Component, Vue, Prop } from 'vue-property-decorator'
// types
import { ArticleData } from '~/types/ArticleData'

@Component
export default class Article extends Vue {
  @Prop() readonly article!: ArticleData

  mounted(){
    const articleElement = this.$refs.article as HTMLElement
    articleElement.onclick = ()=>{
      this.$emit('clicked-article', this.article.title)
    }
  }
}

</script>


// CSS CONTENT
<style scoped>
article {
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.4);
  padding: 15px;
  margin: 30px 0px;
  cursor: pointer;
  transition: all .3s ease;
}
article:hover{
  opacity: 0.5;
}
</style>
