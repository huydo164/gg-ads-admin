<template>
  <div class="article">
    <div class="adsense-detail">
      <span style="font-size: 40px">This for Advertisement</span>
    </div>
    <div class="article__list">
      <b-container>
        <b-row>
          <b-col
            cols="6"
            v-for="item in data"
            :key="item.id"
            class="article__list-item"
          >
            <div class="article__list-item-img">
              <img :src="getImagePath(item)" :alt="item.title" />
            </div>
            <h4>{{ item.title }}</h4>
          </b-col>
        </b-row>
      </b-container>
    </div>
    <b-pagination
      v-model="currentPage"
      :total-rows="total"
      :per-page="perPage"
    ></b-pagination>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      data: [],
      currentPage: 0,
      total: 0,
      perPage: 0,
    };
  },

  mounted() {
    this.fetch();
  },

  methods: {
    async fetch() {
      try {
        const { data } = await axios.get("http://127.0.0.1:8000/api/article");
        this.data = data.data;
        this.currentPage = data.meta.current_page;
        this.total = data.meta.total;
        this.perPage = data.meta.per_page;
      } catch (error) {
        console.error(error);
      }
    },

    getImagePath(item) {
      return /(http(s?)):\/\//i.test(item.image_path) ? item.image_path : "";
    },
  },
};
</script>

<style>
.adsense-detail {
  width: 100%;
  height: auto;
  text-align: center;
  line-height: auto;
}
.article__list-item-img {
  width: 30%;
}
.article__list-item-img img {
  width: 100%;
}
</style>
