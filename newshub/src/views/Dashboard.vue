<template>
  <div class="container-fluid">
    <div class="row">
      <!-- navbar -->
      <div class="col-2 min-vh-100 text-white" id="filterbar">
     

        <h4 class="mb-3 mt-2">Filter</h4>
        <hr />
        <div>
          <b-form @submit.prevent="filterHandler">
            <b-form-group label="Keywords">
              <b-form-input
                type="text"
                placeholder="Enter keyword"
                v-model="keywords"
              ></b-form-input>
            </b-form-group>

            
            <b-button type="submit" variant="primary">Filter</b-button>
          </b-form>
        </div>
        <hr />
        <div class="col">
          <b-button variant="success" @click="alternativeFetch">NYT news source</b-button>
          <!-- <router-link to="/">Home</router-link> -->

          <!-- <a class="row mb-2" href="">Movie List</a>
          <a class="row mb-2" href="">Movie History</a>
          <a class="row mb-2" href="">Create Movie</a> -->
        </div>
        <hr />
        
      </div>

      <div class="col-10">
        <div class="mt-3" v-if="!alternativeNews">
          <card v-for="article in fetchedNews.data" :key="article.url" v-bind:article="article" ></card>
        </div>
        <div class="mt-3" v-if="alternativeNews">
          <card v-for="article in fetchedNews" :key="article.url" v-bind:article="article" ></card>
        </div>
          
        <!-- <b-row cols="3">
          
        </b-row> -->
      </div>
    </div>
  </div>
</template>

<script>
import card from "../components/Card.vue"
import {mapActions, mapState} from "vuex";


export default {
    name: "Dashboard",
    components: {card},
    data() {
        return {
            keywords: "",
            alternativeNews: false,
        }
    },
    computed: {
        ...mapState(["fetchedNews"])
    },
    methods: {
        ...mapActions(["fetchNews", "alternativeFetchNews"]),
        filterHandler() {
            // console.log(this.keywords);
            this.fetchNews(this.keywords)
        },
        async alternativeFetch() {
          await this.alternativeFetchNews(),
          this.alternativeNews = true
        }
    },
    async created() {
        await this.fetchNews()
    }
}
</script>

<style>
    #filterbar {
  background-color: #2c3e50;
}

#filterbar > div a {
  text-decoration: none;
  color: white;
  /* margin-left: 1px; */
}
</style>