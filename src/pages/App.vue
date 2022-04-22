<script>
import { createApi } from 'unsplash-js';
import pictureItem from "../components/pictureItem.vue";

const unsplash = createApi({
  accessKey: 'gS8P7-Hbi_eU8FJqGgOKyExABtWTtwwyz7-5L5LY6Io',
});

export default {
  name: 'App',
  components: {pictureItem},
  data() {
    return {
      photosData: [],
      pageNumber: 1,
    }
  },
  watch: {
    pageNumber: function () {
      this.photosData = unsplash.search
          .getPhotos({
            query: "cat",
            page: this.pageNumber,
            perPage: 10,
          })
          .then(result => this.photosData = result.response)
    }
  },
  mounted() {
    this.photosData = unsplash.search
        .getPhotos({
          query: "cat",
          page: 1,
          perPage: 10,
        })
        .then(result => this.photosData = result.response)

  },
  methods: {
    changePage(newPage) {
      this.pageNumber = +newPage
    }
  },
}

</script>

<template>
  <div class="appWrapper">
    <div class="appBody">
      <picture-item v-for="item in this.photosData.results"
                    :photoData="item">
      </picture-item>
    </div>
    <footer class="appFooter">
      <div  v-if="pageNumber > 2 && pageNumber < 58"
            class="appFooter__pages">
        <div @click="changePage(1)">1</div>
        &nbsp&nbsp...&nbsp&nbsp
        <div class="appFooter__currentPages">
          <div @click="changePage(pageNumber - 1)">{{pageNumber - 1}}&nbsp&nbsp</div>
          <div class="appFooter__boldPage">{{pageNumber}}&nbsp&nbsp</div>
          <div @click="changePage(pageNumber + 1)">{{pageNumber + 1}}</div>
        </div>
        &nbsp&nbsp...&nbsp&nbsp
        <div @click="changePage(59)">59</div>
      </div>
      <div v-if="pageNumber <= 2"
           class="appFooter__pages">
        <div @click="changePage(1)">1&nbsp&nbsp</div>
        <div @click="changePage(2)">2&nbsp&nbsp</div>
        <div @click="changePage(3)">3</div>
        &nbsp&nbsp...&nbsp&nbsp
        <div @click="changePage(59)">59</div>
      </div>
      <div v-if="pageNumber >= 58"
           class="appFooter__pages">
        <div @click="changePage(1)">1</div>
        &nbsp&nbsp...&nbsp&nbsp
        <div @click="changePage(57)">57&nbsp&nbsp</div>
        <div @click="changePage(58)">58&nbsp&nbsp</div>
        <div @click="changePage(59)">59</div>
      </div>
    </footer>
  </div>
</template>

<style lang="scss">
@import '../assets/base.scss';

.appWrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.appBody {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  @include _480 {
    padding-right: 20px;
    padding-left: 20px;
  }
  @include _768 {
    padding-right: 54px;
    padding-left: 54px;
    flex-direction: row;
    flex-wrap: wrap;
  }
  @include _1000 {
    padding-right: 170px;
    padding-left: 170px;
    flex-direction: row;
    flex-wrap: wrap;
  }
}
.appFooter {
  display: flex;
  justify-content: center;
  align-items: center;
  position: sticky;
  bottom: 0;
  min-width: 100%;
  height: 60px;
  background-color: rgba(0, 0, 0, 0.9);
}
.appFooter__pages {
  display: flex;
  align-items: flex-end;
  position: sticky;
  font-family: "Roboto Condensed", sans-serif;
  font-weight: 400;
  font-size: 14px;
  color: #FFFFFF;
}
.appFooter__currentPages {
  display: flex;
  align-items: flex-end;
}
.appFooter__boldPage {
  display: flex;
  align-self: flex-end;
  font-size: 18px;
}
.appFooter > div {
  cursor: pointer;
}
</style>
