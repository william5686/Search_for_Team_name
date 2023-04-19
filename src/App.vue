<script>
  

  import VueGoodTable from 'vue-good-table';

  export default {
    name: 'TeamSearch',
    components: {
      VueGoodTable
    },
    data() {
      return {
        searchTerm: '',
        teams: [],
        columns: [
          {
            label: 'Nombre',
            field: 'name',
            filterable: true,
            sortable: true
          },
          {
            label: 'País',
            field: 'country',
            filterable: true,
            sortable: true
          },
          {
            label: 'Liga',
            field: 'league',
            filterable: true,
            sortable: true
          }
        ]
      }
    },
    methods: {
      async searchTeams() {
        const response = await fetch(`https://futdb.app/api/clubs?name=${this.searchTerm}`);
        const data = await response.json();
        this.teams = data;
      }
    }
  }
</script>







<template>
  <div>
    <label for="team-name">Team name:</label>
    <input type="text" id="team-name" v-model="searchTerm">
    <br>
    <button @click="searchTeams">search</button>

    <vue-good-table :columns="columns" :rows="teams" :paginate="true" :search-options="{ enabled: true }"></vue-good-table>
  </div>
</template>










