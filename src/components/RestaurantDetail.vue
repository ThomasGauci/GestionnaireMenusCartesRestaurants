<template>
<div>
  <div>
  <p v-if="selectedImage"><img style="width:100%" :src="selectedImage" alt=""></p>
</div>
  <md-table v-model="restaurants">
            <md-table-row slot="md-table-row" >
                <md-table-cell>Detail du restaurant d'id</md-table-cell>
                <md-table-cell>{{ id }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Adresse</md-table-cell>
                <md-table-cell>{{ address }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Longitude</md-table-cell>
                <md-table-cell>{{ longitude }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Latitude</md-table-cell>
                <md-table-cell>{{ latitude }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Quartier</md-table-cell>
                <md-table-cell>{{ quartier }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Notes</md-table-cell>
                <md-table-cell>{{ note1 }} {{ note2 }} {{ note3 }} {{ note4 }}</md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>Scores</md-table-cell>
                <md-table-cell>{{ score1 }} {{ score2 }} {{ score3 }} {{ score4 }}</md-table-cell>
            </md-table-row>
        </md-table>
        <h1>CARTES</h1>
        <h1>HORS D'OEUVRES</h1>
        <md-table v-model="cartes">
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{h1[0]}}</md-table-cell>
                <md-table-cell>{{h1[1]}}€</md-table-cell>
                <md-table-cell>{{h1[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="h1[3]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{h2[0]}}</md-table-cell>
                <md-table-cell>{{h2[1]}}€</md-table-cell>
                <md-table-cell>{{h2[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="h2[3]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{h3[0]}}</md-table-cell>
                <md-table-cell>{{h3[1]}}€</md-table-cell>
                <md-table-cell>{{h3[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="h3[3]" alt=""></md-table-cell>
            </md-table-row>
        </md-table>
        <h1>PLATS</h1>
        <md-table v-model="cartes">
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{p1[0]}}</md-table-cell>
                <md-table-cell>{{p1[1]}}€</md-table-cell>
                <md-table-cell>{{p1[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="p1[3]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{p2[0]}}</md-table-cell>
                <md-table-cell>{{p2[1]}}€</md-table-cell>
                <md-table-cell>{{p2[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="p2[3]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{p3[0]}}</md-table-cell>
                <md-table-cell>{{p3[1]}}€</md-table-cell>
                <md-table-cell>{{p3[2]}}</md-table-cell>
                <md-table-cell><img style="width:50%" :src="p3[3]" alt=""></md-table-cell>
            </md-table-row>
        </md-table>
        <h1>DESSERTS</h1>
        <md-table v-model="cartes">
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{d1[0]}}</md-table-cell>
                <md-table-cell>{{d1[1]}}€</md-table-cell>
                <md-table-cell><img style="width:25%" :src="d1[2]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{d2[0]}}</md-table-cell>
                <md-table-cell>{{d2[1]}}€</md-table-cell>
                <md-table-cell><img style="width:25%" :src="d2[2]" alt=""></md-table-cell>
            </md-table-row>
            <md-table-row slot="md-table-row" >
                <md-table-cell>{{d3[0]}}</md-table-cell>
                <md-table-cell>{{d3[1]}}€</md-table-cell>
                <md-table-cell><img style="width:25%" :src="d3[2]" alt=""></md-table-cell>
            </md-table-row>
        </md-table>

  </div>
  
  
</template>

<script>
import _ from 'lodash';

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
      cartes:null,
      restaurants:null,
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
      images: [
      'https://image.noelshack.com/fichiers/2020/02/7/1578861665-terrasse.jpg',
      'https://image.noelshack.com/fichiers/2020/02/7/1578861610-veranda.jpg',
      'https://image.noelshack.com/fichiers/2020/02/7/1578861561-getlstd-property-photo.jpg',
      'https://image.noelshack.com/fichiers/2020/02/7/1578861365-araz-restaurant-interior.jpg',
      'https://image.noelshack.com/fichiers/2020/02/7/1578861305-a1a8429.jpg',
      'https://image.noelshack.com/fichiers/2020/02/7/1578861265-restaurant-araz.jpg'
      ],
      selectedImage: null,
      horsDoeuvres:[
        ['carpaccio de saumon','15','servi avec sa roquette et ses copeaux de parmesan','https://image.noelshack.com/fichiers/2020/02/7/1578864185-recette-e15563-carpaccio-de-saumon-et-avocat.jpg'],
        ['assiette du soleil','15,50','assortiment de légumes grillés et mozzarella, huile d olives','https://image.noelshack.com/fichiers/2020/02/7/1578864218-assiette-du-soleil.jpg'],
        ['tartare de saumon','16','servi avec sa salade du jardin, sa purée d avocat et son zeste de citron','https://image.noelshack.com/fichiers/2020/02/7/1578864257-325986-1050831348.jpg',],
        ['salade de chèvre chaud','13','servi sur son toast avec une pointe de miel','https://image.noelshack.com/fichiers/2020/02/7/1578864302-gd-recette-salade-chevre-chaud.jpg',],
        ['boule de mozarella','8','à l huile d olive et au zeste de citron','https://image.noelshack.com/fichiers/2020/03/1/1578920171-041a5851faacea4340133df08a3760d0.jpg',],
        ['camembert rôti au miel','15','servi avec son pain chaud et sa roquette','https://image.noelshack.com/fichiers/2020/02/7/1578864396-camembert-roti-1000x500.jpg',]
      ],
      plats:[
        ['la norvégienne','15','salade, tomates, saumon fumé, roquette, fenouil, filet d orange','http://www.subitopizza.fr/wp-content/uploads/2013/11/ZenSushi_200903064958.jpg'],
        ['gratin florentina','14','béchamel, pomme de terre, saumon, épinard','https://image.noelshack.com/fichiers/2020/02/7/1578864606-148927.jpg'],
        ['filet de daurade','24','duo de purée de pommes de terre et purée de potimarron','https://image.noelshack.com/fichiers/2020/02/7/1578864606-recette-e2980-filet-de-daurade-royale-au-miel-de-soja-puree-grand-chef.jpg',],
        ['4 fromages','14','sauce tomate, mozzarella, chèvre, ricotta,bleu','https://image.noelshack.com/fichiers/2020/02/7/1578864606-gettyimages-954475908.jpg',],
        ['Arrabiata','12','sauce tomate, piment','https://image.noelshack.com/fichiers/2020/02/7/1578864606-3ce999fde2a859c56aa755cade1e6c14.jpg',],
        ['tournedos rossini','25','foie gras maison accompagné de frites de patate douces','https://image.noelshack.com/fichiers/2020/02/7/1578864606-tournedos-rossini-6-sur-6.jpg',]
      ],
      desserts:[
        ['tiramisu','8','https://image.noelshack.com/fichiers/2020/02/7/1578864840-tiramisu.jpg'],
        ['crème brulée','8','https://image.noelshack.com/fichiers/2020/02/7/1578864841-creme-brulee-vanille-800x516.jpg'],
        ['fondant au chocolat','8','https://image.noelshack.com/fichiers/2020/02/7/1578864841-fondant-au-chocolat.jpg'],
        ['panna cotta','8','https://image.noelshack.com/fichiers/2020/02/7/1578864841-panna-cotta-chocolat-blanc-framboises.jpg'],
        ['mousse au chocolat','8','https://image.noelshack.com/fichiers/2020/02/7/1578864841-recette-mousse-au-chocolat.jpg'],
        ['tarte aux pommes','8','https://image.noelshack.com/fichiers/2020/02/7/1578864841-tarte-aux-pommes.jpg']
      ],
      h1:null,
      h2:null,
      h3:null,
      p1:null,
      p2:null,
      p3:null,
      d1:null,
      d2:null,
      d3:null,
      nbPagesDeResultats:0,
      quartier:"",
      max:6,
      apiURL: "http://localhost:8080/api/restaurants/"
      
    };
  },
  mounted() {
    console.log("AVANT AFFICHAGE !");
    console.log("On va chercher les détails du restaurant id = " + this.$route.params.id);
    console.log("ID = " + this.id);
    this.getDataFromServer();
    let tab = new Array(this.plats.length).fill(0).map((_, i) => _+i);
    tab = _.shuffle(tab);
    console.log(tab)
    this.selectedImage = this.randomItem(this.images)

    this.h1 = this.horsDoeuvres[tab[0]]
    this.h2 = this.horsDoeuvres[tab[1]]
    this.h3 = this.horsDoeuvres[tab[2]]

    this.p1 = this.plats[tab[0]]
    this.p2 = this.plats[tab[1]]
    this.p3 = this.plats[tab[2]]

    this.d1 = this.desserts[tab[0]]
    this.d2 = this.desserts[tab[1]]
    this.d3 = this.desserts[tab[2]]
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
    randomItem (items) {
      return items[Math.floor(Math.random()*items.length)];
    },
    randomNumber(){
      return Math.floor(Math.random()*this.max);
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
