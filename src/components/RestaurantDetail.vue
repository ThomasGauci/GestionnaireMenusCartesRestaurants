<template>
<div>
  <h1>Detail du restaurant d'id = {{id}}</h1>
  <h1>Adresse du restaurant = </h1>
  <h1>Description du quartier = </h1>
  <h1>Evaluation des clients = </h1>

    <!--<md-table-toolbar>
      <div class="md-toolbar-section-start">
          <h1 class="md-title">Test</h1>
      </div>

      <md-field md-clearable class="md-toolbar-section-end">
        <md-input placeholder="Essayons..." v-model="nomRecherche" @input="getDataFromServer()" />
      </md-field>
    </md-table-toolbar>-->

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
    }
  },
  data: function() {
    return {
      
    };
  },
  mounted() {
    console.log("AVANT AFFICHAGE !");
    console.log("On va chercher les détails du restaurant id = " + this.$route.params.id)
    console.log("ID = " + this.id);
  },
  methods: {
    getDataFromServer() {
      // ici on fait un fetch pour récupérer le détail du restaurant

    },
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
