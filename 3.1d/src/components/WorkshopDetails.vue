<template>
<div  class="block">
    <div class="main-left">
        <ul class="main-text">
            <h3 class="h3-link" @click="toggleText(selectedWorkshop.name)">{{ selectedWorkshop.name }}</h3>
            <li class="main-li" v-if="selectedWorkshop.show">{{ selectedWorkshop.text }}</li>
            <div class="booking-container">
                <div class="booking">
                  <div class="booking-left">
                    <div class="booking-text">Next Date:<br>{{ formatDate(selectedWorkshop.date) }}</div>
                    </div>
                    <button class="button button2" @click="redirectToExternalLink">Book Now</button>
                </div>
            </div>
        </ul>  
    </div>
    <div class="main-right">
        <div class="main-opaque">
            <img class="about-img" :src="`/${ selectedWorkshop.image }.png`"/>
        </div>
    </div> 
</div>
<div class="block" v-for="workshop in otherWorkshops" :key="workshop.name">
   <div class="main-left">
        <ul class="main-text">
            <h3 class="h3-link" @click="toggleText(workshop.name)">{{ workshop.name }}</h3>
            <li class="main-li" v-if="workshop.show">{{ workshop.text }}</li>
            <div class="booking-container">
                <div class="booking">
                  <div class="booking-left">
                    <div class="booking-text">Next Date:<br>{{ formatDate(workshop.date) }}</div>
                    </div>
                    <button class="button button2" @click="redirectToExternalLink">Book Now</button>
                </div>
            </div>
        </ul>  
    </div>
    <div class="main-right">
        <div class="main-opaque">
            <img class="about-img" :src="`/${ workshop.image }.png`"/>
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        selectedWorkshop: Object,
        workshops: Array,
    },
    methods: {
        toggleText(name) {
        // Find the workshop with the given name in workshops array
            const workshop = this.workshops.find(workshop => workshop.name === name);
            if (workshop) {
                // Toggle the 'show' property of the found workshop
                workshop.show = !workshop.show;
            }
        },
        formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' };
        return new Date(date).toLocaleDateString('en-UK', options);
        },
        redirectToExternalLink() {
        window.location.href = 'https://www.eventbrite.com.au/d/australia--tasmania/events/';
    }
    },
    
    computed: {
        otherWorkshops() {
            return this.workshops.filter((workshop) => {
                return this.isOther || workshop.name !== this.selectedWorkshop.name;
            });
        }
    }
  }
</script>