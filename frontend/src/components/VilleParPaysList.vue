<template>
  <div>
    <table class="table table-bordered table-sm table-hover">
      <thead>
        <tr>
          <th>Nom</th>
          <th>Population</th>        
        </tr>
      </thead>
      <tbody>
        <tr v-for="city in cities" :key="city.id">
          <td>{{ city.name }}</td>
          <td>{{ city.population }}</td>
          <button
              class="btn btn-sm btn-outline-danger"
              @click="deleteCity(city)"
            >
              Supprimer
            </button>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";
const props = defineProps({
  cities: {
    type: Array,
    required: true,
  },
});

function deleteCity(city) {
  console.log(city);
  const options = {
    method: "DELETE",
  };
  fetch(city._links.self.href, options)
    .then((response) => {
      if (!response.ok) { // status != 2XX
        throw new Error(response.status);
      }
    })
    .catch((error) => alert(error));  
}


</script>
