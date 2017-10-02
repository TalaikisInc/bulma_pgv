<template>
<div class="container is-light">
  <div class="columns">
    
    <div class="column is-two-third">
      <ad-component></ad-component>
      <div class="columns" v-for="(chunk, index) in chunkPosts" :key="'p-' + index">
        <div class="column is-half" v-for="(post, i) in chunk" :key="index + i">
          <div class="card">
            <div class="card-image" v-if="post.image">
              <figure class="image is-4by3">
                <a :href="baseUrl + post.slug + '/'"><img :src="imgBaseUrl + post.image" :alt="post.title"></a>
              </figure>
            </div>
            <div class="card-content">
              <p class="title is-5">
                <a :href="baseUrl + keyword + '/' + post.category_id.Slug + '/'">{{ post.category_id.Title }}</a>
                  | {{ post.date | formatDate }}
              </p>
              <h1 class="title is-3"><a :href="baseUrl + post.slug + '/'">{{ post.title }}</a></h1>
              <div class="content">
                <p v-if="post.content">{{ post.content | truncate }}</p>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-half" v-if="index === (3 || 7)">
          <ad-component></ad-component>
        </div>
      </div>
      <paginator-component v-once :totalPages="calcPages" :paginatorType="paginatorType" value="" :currentPage="page" :itemsPerPage="itemsPerPage" :totalItems="posts[0].total_posts">
      </paginator-component>
    </div>
    
  </div>
</div>
</template>

<script>
import chunk from '../plugins/chunk'
import Paginator from '../components/Paginator.vue'
import Ads from '../components/Ads.vue'
import axios from 'axios'

export default {
  data () {
    return {
      posts: [],
      baseUrl: process.env.BASE_URL,
      imgBaseUrl: process.env.IMG_URL,
      title: process.env.SITE_NAME,
      keyword: process.env.KEYWORD,
      page: null,
      paginatorType: 0,
      itemsPerPage: 20
    }
  },
  asyncData ({ req, params, error }) {
    return axios.get('/posts/' + (Number(params.page) || '0') + '/')
      .then((response) => {
        return { posts: response.data, page: Number(params.page) || 0 }
      })
      .catch((e) => {
        error({ statusCode: 500, message: e })
      })
  },
  components: {
    'paginator-component': Paginator,
    'ad-component': Ads
  },
  computed: {
    chunkPosts () {
      return chunk(this.posts, 2)
    },
    calcPages () {
      const pages = Math.floor(this.posts[0].total_posts / 20)
      return pages <= 250 ? pages : 250
    }
  },
  head () {
    return {
      title: Number(this.$route.params.page) ? 'Page ' + Number(this.$route.params.page) + ' | ' + this.title : this.title
    }
  }
}
</script>
