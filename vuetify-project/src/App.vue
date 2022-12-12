<template>
  <v-app>

  <v-card
    class="mx-auto"
    max-width="1024"
  >
    <v-toolbar
      color="indigo"
      dark
    >


          <v-spacer></v-spacer>
      <v-spacer></v-spacer>
      <v-spacer></v-spacer>


      <v-text-field
            label="API Key"
            placeholder="Insert your API here"
            solo
          ></v-text-field>
    </v-toolbar>

    <v-container fluid>
      <v-row dense>
        <v-col
          v-for="item in workshopItems"
          :key="item.name"
          :cols="3"
        >
          <v-card class="ma-4">
            <v-img
              :src="item.previewUrl"
              class="white--text align-end"
              cover
              gradient="rgba(0,0,0,0), rgba(0,0,0,.4)"
              height="200px"
            >
              <v-card-title style="color:white" v-text="item.name"></v-card-title>
            </v-img>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn icon>
                <v-icon>mdi-heart</v-icon>
              </v-btn>

              <v-btn icon>
                <v-icon>mdi-bookmark</v-icon>
              </v-btn>

              <a v-bind:href=item.steamPage style="text-decoration: none; color: inherit">
                <v-btn icon>
                  <v-icon>mdi-steam</v-icon>
                </v-btn>
              </a>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</v-app>
</template>

<script>
import axios from "axios"
export default{
  name:"App",
  data(){
    return {
      workshopItems:[]
    }
  },
  async mounted(){
    this.workshopItems = (await axios.get("https://marbleraceworkshop.azurewebsites.net/api/QueryItems?limit=10")).data;
    this.workshopItems.forEach((item) => { 
      item.steamPage = "https://steamcommunity.com/sharedfiles/filedetails/?id=" + item.id;
      })
  }
}

</script>
