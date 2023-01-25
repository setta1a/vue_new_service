<template>
  <v-app>
    <v-app-bar color="blue darken" dark app>
      <v-app-bar-nav-icon @click="navigation = !navigation">
      </v-app-bar-nav-icon>
      <v-toolbar-title>НОВОСТИ!! Лучшие новости!!!</v-toolbar-title>
    </v-app-bar>
    <v-navigation-drawer v-model="navigation" absolute temporary>
      <v-select
          :items="countries"
          label="Код страны"
          solo
          v-model="country"
        ></v-select>
        <v-text-field
            v-model="keywords"
            label="Ключевые слова"
        ></v-text-field>
        <v-btn
          color="primary"
          block
          @click="getNews"
        >
          Получить новости
        </v-btn>
    </v-navigation-drawer>
    <v-main>
      <template>
        <v-container class="grey lighten-5">
          <v-row no-gutters>
            <v-col 
            v-for="arcticle, index in news" 
            :key="index" 
            cols="12" 
            sm="4">
              <v-card class="pa-2 ma-2">
                <v-img :src="arcticle.urlToImage" class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)" height="200px">
                  <v-card-title>{{ arcticle.title }}</v-card-title>
                </v-img>
                <v-card-text>
                  <p v-if="arcticle.content">
                    {{ arcticle.content }}
                  </p>
                  <p v-else>
                    Lorem ipsum, dolor sit amet consectetur adipisicing elit. Tempora repellat vitae incidunt odio sint deleniti? Odit, nihil quae! Ducimus iusto fugit laboriosam soluta odio repudiandae vero nam labore facilis accusamus.
                  </p>
                </v-card-text>
                <v-card-actions>

                  <v-btn variant="outlined" :href="arcticle.url">
                     Читать полностью 
                  </v-btn>
                  <v-spacer></v-spacer>
                  <v-btn icon>
                    <v-icon>mdi-heart</v-icon>
                  </v-btn>

                  <v-btn icon>
                    <v-icon>mdi-bookmark</v-icon>
                  </v-btn>

                  <v-btn icon>
                    <v-icon>mdi-share-variant</v-icon>
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </template>
    </v-main>
  </v-app>
</template>

<script>


export default {
  name: 'App',

  components: {
  },

  data: () => ({
    navigation: false,
    news: [],
    countries: ["ae", "ar", "at", "au", "be", "bg", "br", "ca", "ch", "cn", "co", "cu", "cz", "de", "eg", "fr", "gb", "gr", "hk", "hu", "id", "ie", "il", "in", "it", "jp", "kr", "lt", "lv", "ma", "mx", "my", "ng", "nl", "no", "nz", "ph", "pl", "pt", "ro", "rs", "ru", "sa", "se", "sg", "si", "sk", "th", "tr", "tw", "ua", "us", "ve", "za"],
    country: "us",
    keywords: ""
  }),
  methods: {
    getNews() {
      this.axios({
        method: "GET",
        url: `https://newsapi.org/v2/top-headlines?country=${this.country}&apiKey=d7f41a32c26b4bbfb596d58b1a54c766&q=${this.keywords}`
      }).then((response)=> {
        this.news = response.data.articles
        console.log(response.data.articles)
      })
    }
  },
  mounted() {
    this.getNews()
  }
};
</script>
