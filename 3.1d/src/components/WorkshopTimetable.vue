<template>
  <div class="content">
    <h3>Coming up:</h3>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Workshop</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through each workshop in sortedWorkshops -->
        <tr v-for="(workshop, index) in workshops" :key="index">
          <td>{{ formatDate(workshop.date) }}</td> <!-- Display formatted workshop date -->
          <td>
            <a @click="selectWorkshop(workshop.name)" class="workshop-a">{{ workshop.name }}</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
    props: {
        workshops: Array, // Define the workshops prop to receive the sorted workshops data
    },
    methods: {
        selectWorkshop(workshopName) {
        // Emit an event or update a data property with workshopName
        this.$emit('workshopSelected', workshopName);
        },
        toggleText(index) {
        this.workshops[index].show = !this.workshops[index].show;
        },
        formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' };
        return new Date(date).toLocaleDateString('en-UK', options);
        },
    },
  }
</script>

  <style scoped>
  /* Scoped styles for the component */
  th, td {
    border: 1px solid white;
    padding: 12px;
    text-align: center;
    background-color: white;
    color: black;
  }
  
  th {
    font-weight: bold;
    background-color: #0E6251;
    color: white;
  }
  
  .workshop-a {
    color: black;
    text-decoration: none;
    padding: 10px;
    transition: background-color 0.3s;
    cursor: pointer;
  }
  
  .workshop-a:hover {
    background-color: #f0f0f0;
  }
  
  table {
    width: 100%;
  }
  </style>