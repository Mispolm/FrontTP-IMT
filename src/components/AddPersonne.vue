<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <!-- A COMPLETER -->

    <input type="text" class="name" id="name" required v-model="currentPersonne.name" name="name" />
    <input type="text" class="surname" id="surname" required v-model="currentPersonne.surname" name="surname" />
    <input type="text" class="phone" id="phone" required v-model="currentPersonne.phone" name="phone" />
    <input type="text" class="city" id="city" required v-model="currentPersonne.city" name="city" />

      <button @click="creerPersonne" class="btn btn-success">Ajouter</button>
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
        phone:this.personne.phone,
        city:this.personne.city,
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
