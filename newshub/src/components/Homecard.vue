<template>
  <b-card no-body class="overflow-hidden" style="max-width: 540px;">
    <b-row no-gutters>
      <b-col md="6">
        <b-card-img :src="article.imageUrl ? article.imageUrl :'https://picsum.photos/400/400/?image=20'" alt="Image" class="rounded-0"></b-card-img>
      </b-col>
      <b-col md="6">
        <b-card-body :title="article.title">
            <b-button variant="success" @click="detailsHandler">Details</b-button>
            <!-- <b-button variant="primary" @click="publishHandler">Publish</b-button> -->
          <!-- <b-card-text>
            {{article.description}}
          </b-card-text> -->
        </b-card-body>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>


export default {
    name: "Homecard",
    props: ["article"],
    methods: {
        detailsHandler() {
            this.$router.push({name: "ArticleDetail", params: {id: this.article.id}})
        }
    }
}
</script>

<style>

</style>