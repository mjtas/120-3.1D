<template>
  <div class="main">
    <div class="main-container">
      <div class="main-heading">
        <h1>Hidden Valley</h1>
        <h2>Sustainable Living Workshops</h2>
        </div>
        <div class="main-other" v-if="selectedWorkshopName==''">
          <div class="table-left">
          <WorkshopTimetable :workshops="sortedWorkshops" @workshopSelected="handleWorkshopSelected" />
        </div>
        <div class="main-right">
          <ul class="main-text">
            <li class="main-li">Are you looking for inspiration and information to start gardening, bread baking, making compost or building? You might want to extend your knowledge and improve your practical skills. Or you might be travelling in Tasmania and looking for an interesting activity to do while you are here. </li>
            <li class="main-li">Our workshops will inspire you to get out there and start that new hobby or project you want to do, and they are a fun and informative way to spend your Sunday morning! </li>
            <li class="main-li">Hidden Valley is only 20 minutes from Deloraine, an hour from Devonport or Launceston, and 2 hours from Hobart on the Great Lakes touring route.</li>
          </ul>
        </div>
      </div>
      <div class="about-other" v-if="selectedWorkshopName && selectedWorkshopName!==''"> 
        <WorkshopDetails :selectedWorkshop="selectedWorkshop" :workshops="sortedWorkshops"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import WorkshopTimetable from '../components/WorkshopTimetable.vue'
import WorkshopDetails from '../components/WorkshopDetails.vue';

export default {
  components: {
    WorkshopTimetable,
    WorkshopDetails,
  },
  data() {
    return {
      workshops: [], // Store fetched data here
      sortedWorkshops: [], // Store sorted workshops here
      selectedWorkshop: null, //Set initial value to null
      selectedWorkshopName: '', // Set initial value to an empty string
    };
  },
  created() {
    // Make HTTP GET request to backend API
    axios.get('http://localhost:3000/getData')
      .then(response => {
        this.workshops = response.data; // Update workshops property with fetched data
        this.sortWorkshops(); // Sort the workshops
        // Set selectedWorkshop to the first workshop in sortedWorkshops
        this.selectedWorkshop = this.sortedWorkshops[0];
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  },
  methods: {
    handleWorkshopSelected(workshopName) {
      // Handle the selected workshop name emitted from child component
      this.selectedWorkshopName = workshopName;
      this.selectedWorkshop = this.sortedWorkshops.find(workshop => workshop.name === workshopName);
    },
    
    sortWorkshops() {
      // Sort workshops by date in ascending order
      this.sortedWorkshops = [...this.workshops].sort((a, b) => new Date(a.date) - new Date(b.date));
    },
  }
}
</script>