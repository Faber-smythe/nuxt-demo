// HTML CONTENT
<template>
  <main>
    <h1 ref="mainTitle">Hello World</h1>
    <img src="/dvic.png" />
    <div>
      <input ref="slider" type="range" :value="sliderValue" />
      <p class="main-paragraph">
        The above slider currently holds the following value :
        <span class="current-value">{{ sliderValue }}</span>
      </p>
    </div>
    <Article
      v-for="(element, i) in articleList"
      :key="`article-${i}`"
      :article="element"
      @clicked-article="
        (title) => {
          articleClick(title)
        }
      "
    />
    <hr />

    <p class="main-paragraph">
      Amount of clicked articles : <span>{{ articleClicks }}</span>
    </p>
  </main>
</template>

// TYPESCRIPT CONTENT
<script lang="ts">
// import libs
import { Component, Vue } from 'vue-property-decorator'
// import components
import Article from '@/components/Article.vue'
// import types
import { ArticleData } from '@/types/ArticleData'

@Component({
  components: {
    Article
  }
})
export default class Index extends Vue {
  articleClicks = 0
  sliderValue: number | string = 50
  articleList = require('@/assets/articles.json') as ArticleData[]
  mainTitle!: HTMLElement
  slider!: HTMLInputElement

  mounted() {
    this.mainTitle = this.$refs.mainTitle as HTMLElement
    this.slider = this.$refs.slider as HTMLInputElement

    this.updadteTitleShift()

    this.slider.addEventListener('mousemove', () => {
      this.sliderValue = this.slider.value
      this.updadteTitleShift()
    })
  }

  updadteTitleShift() {
    const value = Number(this.slider.value)
    this.mainTitle.style.marginLeft = `${value}px`
    this.mainTitle.style.opacity = String(1 - value / 100)
  }

  articleClick(title: string) {
    console.log('The following article has been clicked : ', title)
    this.articleClicks++
  }
}
</script>

// CSS CONTENT
<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');

html,
body {
  position: relative;
  display: flex;
  justify-content: center;
}
body * {
  font-family: 'Roboto', sans-serif;
}
main {
  width: 33vw;
}
img{
  position: fixed;
  top: 15px;
  right: 15px;
  height: 15vh;
}
input {
  cursor: pointer;
}
.main-paragraph {
  font-size: 1.5em;
}
.current-value {
  font-weight: 500;
}
</style>
