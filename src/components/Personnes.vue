<template>
  
<div class="row">
  <div class="col-sm-4">
    <ul class="list-group">
      <li class="list-group-item"
        :class="{ active: id == currentIndex }"
        v-for="(personne, id) in personnes"
        :key="id"
        @click="setActivePersonne(personne, id)"
        >
        {{ personne.surname }} {{ personne.name }}
      </li>
    </ul>
  </div>

  <div class="col-sm-4">
    <div class="card border-dark mb-3" style="max-width: 30rem;">
      <div class="card-header text-center">Informations</div>
      <div class="card-body text-dark">     
        <div v-if="currentPersonne">
          <li class="list-group-item list-group-item-dark">Nom : 
          {{ currentPersonne.name }}
          </li>
          <li class="list-group-item list-group-item-dark">Prénom :
          {{ currentPersonne.surname }}
          </li>
          <li class="list-group-item list-group-item-dark">Téléphone :
          {{ currentPersonne.phone }}
          </li>  
           <li class="list-group-item list-group-item-dark mb-3">Ville :
          {{ currentPersonne.city }}
           </li>
          <router-link :to="'/personnes/' + currentPersonne.id" class="btn btn-warning rounded-pill
          ">Modifier/Supprimer</router-link>
        </div>
 
        <div v-else>
         <br />
         <p>Cliquez sur une des personnes pour afficher les détails.</p>
        </div>
      </div>         
    </div>
  </div>
</div>
  

</template>

<script>
  import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personnes",
  data() {
    return {
      personnes: [],
      currentPersonne: null,
      currentIndex: -1,
    };
  },
  methods: {
    getPersonnes() {
      PersonneDataService.getAll()
        .then(response => {
          this.personnes = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    setActivePersonne(personne, index) {
      this.currentPersonne = personne;
      this.currentIndex = personne ? index : -1;
    },
  },
  mounted() {
    this.getPersonnes();
  }
};
</script>
