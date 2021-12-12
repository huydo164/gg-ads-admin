<template>
  <div class="adsense-detail">
    <span style="font-size: 40px">This for Advertisement</span>
  </div>
</template>

<script>
import axios from "axios"
export default {
  data () {
    return {
      data: [],
    }
  },

  mounted () {
    this.fetch()
  },

  methods: {
    async fetch () {
      try {
        const { data } = await axios.get('http://127.0.0.1:8000/api/article')
        this.data = data.data

      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
.adsense-detail {
  width: 100%;
  height: auto;
  text-align: center;
  line-height: auto;
}
</style>
