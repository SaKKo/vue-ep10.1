<template lang="html">
  <div class="container">
    Manga Search Page
    <Input
      v-model="query"
      placeholder="Enter something..."
      style="width: 100%"
    />
    <Button type="primary" style="margin-top: 20px" @click="handleSearchManga">
      Search Manga
    </Button>
    <Divider></Divider>
    <Row :gutter="16" type="flex" justify="center">
      <Col
        v-for="manga in results"
        :key="manga.mal_id"
        style="width: 300px; margin-top: 10px;"
      >
        <div @click="handleMangaClick(manga)">
          <Card>
            <p slot="title">{{ manga.title }}</p>
            <Row>
              <Col :span="16">
                <p style="width: 100%;">
                  {{ manga.synopsis }}
                </p>
              </Col>
              <Col :span="8">
                <img :src="manga.image_url" alt="" style="width: 100%;" />
              </Col>
            </Row>
          </Card>
        </div>
      </Col>
    </Row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: 'Dragon',
      results: []
    }
  },
  methods: {
    handleSearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      axios.get(url).then((response) => {
        this.results = response.data.results
      })
    },
    handleMangaClick(manga) {
      window.location = manga.url
    }
  }
}
</script>

<style lang="css" scoped>
.container {
  margin: 40px 60px;
}
</style>
