<template>
  <div class="is-fluid">
    <div class="container">
      <nav class="navbar level is-info">
        <div class="navbar-brand">
          <div class="navbar-burger burger" data-target="navMenu">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </div>
        <div id="navMenu" class="navbar-menu">
          <div class="navbar-start">
            <div class="navbar-item has-dropdown is-hoverable">
              <a class="navbar-link  is-active" href="#">
                Categories
              </a>
              <div class="navbar-dropdown is-boxed">
                <a class="navbar-item" v-for="(cat, index) in categories" :index="'1-' + index" :key="'1-' + index" :href="baseUrl + keyword + '/' + cat.slug + '/'">
                  {{ cat.title }} [{{ cat.post_count }}]
                </a>
                <hr class="navbar-divider">
                <div class="navbar-item">
                  <strong class="has-text-info">
                    <a :href="baseUrl + catKey + '/1/'">
                      All categories
                    </a>
                  </strong>
                </div>
              </div>
            </div>
            <div class="navbar-item has-dropdown is-hoverable">
              <a class="navbar-link  is-active" href="#">
                Trending
              </a>
              <div class="navbar-dropdown is-boxed">
                <a :href="baseUrl + searchKey + '/keyword/'">
                  Keyword
                </a>
              </div>
            </div>
          </div>
        </div>
        <div class="navbar-end">
          <a class="navbar-item" :href="'https://twitter.com/' + twHandle" target="_blank">
            <i class="fa fa-lg fa-twitter"></i>
          </a>
          <a class="navbar-item" :href="'https://www.facebook.com/' + fbHandle" target="_blank">
            <i class="fa fa-lg fa-facebook"></i>
          </a>
        </div>
      </nav>
      <section class="hero is-info">
        <div class="hero-body">
          <div class="container">
            <a :href="baseUrl" :title="title">
              <img src="~/assets/logo/logo.png" class="img-pad" width="90px" height="90px" :alt="title">
            </a>
            <h1 class="title is-1">
              {{ title }}
            </h1>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'headerComponent',
  data () {
    return {
      categories: this.categories,
      baseUrl: process.env.BASE_URL,
      logoAlt: process.env.SITE_NAME,
      title: process.env.SITE_NAME,
      keyword: process.env.KEYWORD,
      catKey: process.env.CATEGORIES_KEY,
      searchKey: process.env.SEARCH_KEYWORD,
      twHandle: process.env.TWITTER_HANDLE,
      fbHandle: process.env.FACEBOOK_HANDLE
    }
  },
  methods: {
    fetchData () {
      axios.get('/cats/0/').then(response => {
        this.categories = response.data
      }).catch(e => {
        console.log(e)
      })
    }
  },
  mounted () {
    this.fetchData()
  }
}
</script>

<style>
</style>