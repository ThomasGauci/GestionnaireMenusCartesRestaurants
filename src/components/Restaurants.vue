<template>
<div>
  <p>
    Rechercher par nom:
    <input type="text" v-model="nomRecherche" v-on:input="getDataFromServer()" />
  </p>
  <p>
    Nombre de restaurants par page :
    <input
      type="range"
      min="2"
      max="100"
      value="10"
      v-on:input="getDataFromServer()"
      v-model="pagesize"
    />
    {{pagesize}}
  </p>
  <h1>Nombre de restaurants : {{nbRestaurants}}</h1>
  <button v-on:click="ajouterRestaurant()"><md-icon>add</md-icon></button>
  <button v-on:click="pagePrecedente()" v-bind:disabled="page==0"><md-icon>arrow_back_ios</md-icon></button>
  <button v-on:click="pageSuivante()" :disabled="page == nbPagesDeResultats"><md-icon>arrow_forward_ios</md-icon></button>
 
  <H1>TABLE VUE-MATERIAL</H1>
        <md-table v-model="restaurants" md-sort="name" md-sort-order="asc" md-card md-fixed-header>
            <md-table-toolbar>
                <div class="md-toolbar-section-start">
                    <h1 class="md-title">Nom cherche</h1>
                </div>

                <md-field md-clearable class="md-toolbar-section-end">
                    <md-input placeholder="Search by name..." v-model="nomRecherche" @input="getDataFromServer()" />
                </md-field>
            </md-table-toolbar>

            <md-table-empty-state
        md-label="No users found"
        :md-description="`No user found for this '${nomRecherche}' query. Try a different search term or create a new user.`">
      </md-table-empty-state>

            <md-table-row slot="md-table-row" slot-scope="{ item }">
                <md-table-cell md-label="Name" md-sort-by="name">{{ item.name }}<md-button class="md-icon-button" v-on:click="changeName(item)"><md-icon>create</md-icon></md-button></md-table-cell>
                <md-table-cell md-label="Cuisine" md-sort-by="cuisine">{{ item.cuisine }}<md-button class="md-icon-button" v-on:click="changeKitchen(item)"><md-icon>create</md-icon></md-button></md-table-cell>
                <md-table-cell md-label="Details"><router-link :to="'restaurant/'+item._id"><md-icon>loupe</md-icon></router-link></md-table-cell>
                <md-table-cell md-label="Supprimer"><md-button class="md-icon-button" v-on:click="supprimerRestaurant(item._id)"><md-icon>delete</md-icon></md-button></md-table-cell>
            </md-table-row>
        </md-table>
  </div>
</template>

<script>
export default {
  name: "Restaurants",
  props: {},
  data: function() {
    return {
      restaurants: [],
      nbRestaurants: 0,
      nom: "",
      cuisine: "",
      page: 0,
      pagesize: 10,
      nomRecherche: "",
      nbPagesDeResultats: 0,
      apiURL: "http://localhost:8080/api/restaurants"
    };
  },
  mounted() {
    console.log("AVANT AFFICHAGE !");
    this.getDataFromServer();
  },
  methods: {
    getDataFromServer() {
      // ici on fait un fetch pour récupérer des
      // restaurants sur le serveur.
      let url =
        this.apiURL +
        "?page=" +
        this.page +
        "&pagesize=" +
        this.pagesize +
        "&name=" +
        this.nomRecherche;

      fetch(url)
        .then(reponseJSON => {
          return reponseJSON.json();
        })
        .then(reponseJS => {
          // ici on a la réponse sous la forme
          // d'un objet JS
          this.restaurants = reponseJS.data;
          this.nbRestaurants = reponseJS.count;
          this.nbPagesDeResultats = Math.floor(
            this.nbRestaurants / this.pagesize
          );
        });
    },
    supprimerRestaurant(index) {
        event.preventDefault();

        let url =
          this.apiURL +
          "/" + index;

      fetch(url, {method: "DELETE"})
        .then(reponseJSON => {
          this.getDataFromServer();
          return reponseJSON.json();
        })
        .catch(console.error);
        //redemander la liste au serveur
        
    },
    ajouterRestaurant() {

      this.$prompt("Ecrivez le nom du nouveau restaurant")
      .then(name_text => {   
        this.$prompt("Ecrivez la cuisine du nouveau restaurant")
        .then(cuisine_text => {

          var formData = new FormData();

          formData.append('nom', name_text);
          formData.append('cuisine', cuisine_text);

          fetch(this.apiURL, {method : "POST", body : formData})
          .then(res => { 
            this.$alert("Vous avez crée le restaurant " + name_text + " !", "Success", "success");
            this.getDataFromServer();
            return res.json();
          })
          .catch(err => {console.error(err)})
        })
      })

    },
    getColor(index) {
      return index % 2 ? "lightBlue" : "pink";
    },
    pageSuivante() {
      console.log("Page suivante");
      this.page++;
      this.getDataFromServer();
    },
    pagePrecedente() {
      console.log("Page precedente");
      this.page--;
      this.getDataFromServer();
    },
    changeKitchen(item){

      this.$prompt("Ecrivez la nouvelle cuisine du restaurant", item.cuisine)
      .then(text => {
        let url =
        this.apiURL +
        "/" + item._id;

        var formData = new FormData();
        formData.append('nom', item.name);
        formData.append('cuisine', text);

        fetch(url, {method: "PUT", body: formData})
        .then(reponseJSON => {
            this.$alert("Vous avez changé la cuisine du restaurant par : " + text, "Success", "success");
            this.getDataFromServer();
            return reponseJSON.json();
        })
        .catch(console.error);
      });
    },
    changeName(item){
      
      this.$prompt("Ecrivez le nouveau nom du restaurant", item.name)
      .then(text => {
       
        var formData = new FormData();
        formData.append('nom', text);
        formData.append('cuisine', item.cuisine);

          let url =
          this.apiURL +
          "/" + item._id;

        fetch(url, {method: "PUT", body: formData})
        .then(reponseJSON => {
          this.$alert("Vous avez changé le nom du restaurant par : " + text, "Success", "success");
          this.getDataFromServer();
          return reponseJSON.json();
        })
        .catch(console.error);
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
