<template>
  <div class="home">
    <h1 class="title">"Tweets"</h1>
    <TweetsComponent v-bind:tweets="items" />
  </div>
</template>

<script>
import ee from '@/event-emitter.js'
import store from '@/store.js'
import TweetsComponent from '@/components/Tweets'

export default {
  name: 'home',
  data: () => ({
    items: []
  }),
  components: {
    TweetsComponent
  },
  methods: {
    getTweets () {
      this.items = store.getTweets()
    }
  },
  created () {
    if (store.state.fetched) {
      this.getTweets()
    } else {
      store.fetch()
    }
    ee.on('api-fetch', this.getTweets)
  }
}
</script>
