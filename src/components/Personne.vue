<template>
  <!-- A COMPLETER -->

    <!-- A INCLURE DANS LE FORM -->

<div class="row">
  <div class="col-sm-4">
    <div class="card border-danger mb-3">
      <div class="card-header text-center">Suppression</div>
      <div class="card-body">
        <div class="card-body text-danger">
        <p class="card-text">Êtes-vous sûr de vouloir supprimer cette personne?</p>
        <button class="btn btn-danger rounded-pill"
        @click="deletePersonne"
        >
        Supprimer
        </button>
        </div>
      </div>
    </div>
  </div> 

  <div class="col-sm-6">
    <div class="card border-primary mb-3">
      <div class="card-header text-center">Modification</div>
      <div class="card-body text-primary">
          <p class="card-text">Veuillez saisir les informations ci-dessous pour mettre à jour la personne</p> 
    
          <li class="list-group-item list-group-item-primary">Nom :   
          <input type="text" class="surname" id="surname" v-model="currentPersonne.name" />       
          </li>
          <li class="list-group-item list-group-item-primary">Prénom :  
          <input type="text" class="surname" id="surname" v-model="currentPersonne.surname" />       
          </li>
          <li class="list-group-item list-group-item-primary">Téléphone :
          <input type="text" class="phone" id="phone" v-model="currentPersonne.phone" />       
          </li>
          <li class="list-group-item list-group-item-primary mb-3">Ville :
          <input type="text" class="phone" id="phone" v-model="currentPersonne.city" />       
          </li>
          <button type="submit" class="btn btn-primary rounded-pill"
          @click="updatePersonne"
          >
          Modifier
          </button>
          <p>{{ message }}</p>
       </div>
    </div>
  </div>
</div>    

 
    
    
    
  
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personne",
  data() {
    return {
      currentPersonne: null,
      message: ''
    };
  },
  methods: {
    getPersonne(id) {
      // A COMPLETER
      PersonneDataService.get(id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    updatePersonne() {
      // A COMPLETER
      PersonneDataService.update(this.currentPersonne)
        .then(response => {
          this.currentPersonne = response.data;
          this.message = 'Personne modifiée avec succès!';
        })
        .catch(e => {
          console.log(e);
        });
    },

    deletePersonne() {
      // A COMPLETER
      PersonneDataService.delete(this.currentPersonne.id)
        .then(response => {
          this.currentPersonne = response.data;
          this.$router.push({ name:"personnes" });
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.message = '';
    this.getPersonne(this.$route.params.id);
  }
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
