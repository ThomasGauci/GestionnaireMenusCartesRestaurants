<template>
<div>
  <md-table v-model="restaurants">
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Detail du restaurant d'id</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ id }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Adresse</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ address }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Longitude</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ longitude }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Latitude</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ latitude }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Quartier</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ quartier }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Notes</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ note1 }} {{ note2 }} {{ note3 }} {{ note4 }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell md-label="Name" md-sort-by="name">Scores</md-table-cell>
                <md-table-cell md-label="Name" md-sort-by="name">{{ score1 }} {{ score2 }} {{ score3 }} {{ score4 }}</md-table-cell>
            </md-table-row>
        </md-table>
  </div>
  
  
</template>

<script>
export default {
  name: "RestaurantDetail",
  props: {},
  computed: { // computed data, permet de définir des data "calculées"
      id() {
        // on y accèdera par {{id}} dans le template, et par this.id
        // dans le code
  
      return this.$route.params.id
    },
  },
  data: function() {
    return {
      restaurant:"",
      nom:"",
      address:"",
      longitude:"",
      latitude:"",
      note1:"",
      note2:"",
      note3:"",
      note4:"",
      score1:"",
      score2:"",
      score3:"",
      score4:"",
      cuisine:"",
      page:0,
      pagesize:10,
      nomrecherche:"",
      image:"",
      nbPagesDeResultats:0,
      quartier:"",
      apiURL: "http://localhost:8080/api/restaurants/"
      
    };
  },
  mounted() {
    console.log("AVANT AFFICHAGE !");
    console.log("On va chercher les détails du restaurant id = " + this.$route.params.id);
    console.log("ID = " + this.id);
    this.getDataFromServer();
  },
  methods: {
    getDataFromServer() {
      // ici on fait un fetch pour récupérer le détail du restaurant
      let url =
      this.apiURL + this.$route.params.id;
      console.log(url);
      fetch(url)
        .then(reponseJSON => {
          return reponseJSON.json();
        })
        .then(reponseJS => {
          // ici on a la réponse sous la forme
          // d'un objet JS
          this.address = reponseJS["restaurant"]["address"]["building"]["restaurant"]+" " + reponseJS["restaurant"]["address"]["street"]
          this.longitude = reponseJS["restaurant"]["address"]["coord"][0]
          this.latitude = reponseJS["restaurant"]["address"]["coord"][1]
          this.note1 = reponseJS["restaurant"]["grades"][0]["grade"]
          this.note2 = reponseJS["restaurant"]["grades"][1]["grade"]
          this.note3 = reponseJS["restaurant"]["grades"][2]["grade"]
          this.note4 = reponseJS["restaurant"]["grades"][3]["grade"]
          this.score1 = reponseJS["restaurant"]["grades"][0]["score"]
          this.score2 = reponseJS["restaurant"]["grades"][1]["score"]
          this.score3 = reponseJS["restaurant"]["grades"][2]["score"]
          this.score4 = reponseJS["restaurant"]["grades"][3]["score"]
          this.quartier = reponseJS["restaurant"]["borough"]
        });
    },
    
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
