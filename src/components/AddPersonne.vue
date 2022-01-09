<template>


<div class="submit-form">
  <div v-if="!submitted">
      <!-- A COMPLETER -->
   
    <div class="input-group mb-3 flex-nowrap">        
      <span class="input-group-text" id="basic-addon1">Nom :</span>
      <input type="text" class="form-control" required v-model="personne.name" placeholder="c'est parti.. :)" aria-label="Nom" aria-describedby="basic-addon1">        
    </div>


    <div class="input-group mb-3 flex-nowrap">
      <span class="input-group-text" id="basic-addon1">Prenom :</span>   
      <input type="text" class="form-control" required v-model="personne.surname" placeholder="encore une fois.." aria-label="Prenom" aria-describedby="basic-addon1">  
    </div>

    <div class="input-group mb-3 flex-nowrap">
      <span class="input-group-text" id="basic-addon1">Telephone :</span>  
      <input type="text" class="form-control" required v-model="personne.phone" placeholder="vous y êtes presque !" aria-label="Telephone" aria-describedby="basic-addon1"> 
    </div>

    <div class="input-group mb-3 flex-nowrap">
      <span class="input-group-text" id="basic-addon1">Ville :</span>   
      <input type="text" class="form-control" required v-model="personne.city" placeholder="une dernière pour la route" aria-label="Ville" aria-describedby="basic-addon1"> 
    </div>

    <div class="d-grid gap-2 col-4 mx-auto">
      <button @click="creerPersonne" class="btn btn-success">Ajouter</button>
    </div>

  </div>

  <div v-else>
    <h4>Personne ajoutée avec succès!</h4>
      <button class="btn btn-success" @click="resetForm">Ajouter une nouvelle personne</button>
  </div>

</div>

</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "add-personne",
  data() {
    return {
      personne: {
        id: null,
        name: "",
        surname: "",
        phone: "",
        city: ""
      },
      submitted: false
    };
  },
  methods: {
    creerPersonne() {
      var data = {
        name: this.personne.name,
        surname: this.personne.surname,
        phone: this.personne.phone,
        city: this.personne.city,

        // A COMPLETER
      };

      // A COMPLETER
      PersonneDataService.create(data)
      .then(response => {
          console.log(response.data);
          this.submitted = true;
        })
          .catch(e => {
          console.log(e);
        });  
    },
    
    resetForm() {
      this.submitted = false;
      this.personne = {};
    }
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
