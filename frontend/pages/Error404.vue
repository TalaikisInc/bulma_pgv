<template>
<div class="container">
  <div class="columns">
    <div class="column is-two-third">
      <h1 class="title is-1">404</h1>
      <div class="content">
        <p>Page not found.</p>
        <a :href="baseUrl">Back to Home</a>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'errorPage',
  data () {
    return {
      baseUrl: process.env.BASE_URL,
      logoAlt: process.env.SITE_NAME
    }
  }
}
</script>

<style>
</style>