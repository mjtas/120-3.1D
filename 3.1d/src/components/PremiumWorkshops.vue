<template>
  <div class="content">
    <table>
      <thead>
        <tr>
          <th>Premium Workshops - $150</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through each workshop in premiumWorkshops -->
        <tr v-for="(workshop, index) in premiumWorkshops" :key="index">
          <td>
            <router-link :to="`/`" class="workshop-a">
              {{ workshop.name }}
            </router-link>
          </td>
        </tr>
      </tbody>
    </table>
    <table>
      <thead>
        <tr>
          <th>Standard Workshops - $110</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through each workshop in premiumWorkshops -->
        <tr v-for="(workshop, index) in standardWorkshops" :key="index">
          <td>
            <router-link :to="`/`" class="workshop-a">
              {{ workshop.name }}
            </router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      workshops: [], // Store fetched data here
    };
  },
  created() {
    // Make HTTP GET request to backend API
    axios.get('http://localhost:3000/getData')
      .then(response => {
        this.workshops = response.data; // Update workshops property with fetched data
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  },
  computed: {
    premiumWorkshops() {
      return this.workshops.filter(workshop => this.isPremium || workshop.premium);
    },
    standardWorkshops() {
      return this.workshops.filter(workshop => this.isStandard || !workshop.premium);
    }, 
  },
};
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
    }
    
    .workshop-a:hover {
      background-color: #f0f0f0;
    }
    
    table {
      width: 100%;
    }
    </style>