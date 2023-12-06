<template>
<div class="main">
  <div class="main-container">
    <div class="main-heading">
      <h1>Hidden Valley</h1>
      <h2>Contact Us</h2>
    </div>
    <div class="about-other">
      <ul class="main-text">
        <li>Phone: 0400 621 126</li>
        <li>Email: hiddenValley@duck.com</li>
        <li>Workshops are held at 12361 Highland Lakes Rd, Golden Valley (gate open during workshops only)</li>
      </ul>
      </div>
    <div class="map" id="map" style="height: 400px; width: 100%; box-sizing: border-box; margin: 0"></div>
    
    <ul class="main-text">
    <h3>Questions about any of our workshops?</h3>
    <li class="main-li">
      <label for="name">Name:</label><br>
      <input type="text" id="name" name="name" v-model="name"><br>
      <label for="user_email">Email Address:</label><br>
      <input type="email" id="user_email" name="email" placeholder="you@example.com" v-model="email" required><br>
      <label for="message">Your enquiry:</label><br>
      <!-- Use textarea for the message input -->
      <textarea class="message-input" id="message" name="message" rows="4" cols="50" v-model="message"></textarea><br>
      <button type="button" class="button button1" @click="submitForm">Send</button>
    </li>
    <br>
    <h3>Subscribe to keep up to date</h3>
    <label for="subscription_name">Name:</label><br>
    <input type="text" id="subscription_name" name="name" v-model="name"><br>
    <label for="subscription_email">Email Address:</label><br>
    <input type="email" id="subscription_email" name="email" placeholder="you@example.com" v-model="email" required><br>
    <fieldset>
      <legend>Subscription options:</legend>
      <input type="checkbox" id="newsletter" name="newsletter" v-model="newsletterChecked">
      <label for="newsletter">Monthly newsletter</label>
      <input type="checkbox" id="workshops" name="workshops" v-model="workshopsChecked">
      <label for="workshops">New workshops</label>
    </fieldset>
    <button type="button" class="button button1" @click="submitForm">Subscribe</button>
  </ul>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      name: '',
      message: '',
      newsletterChecked: true,
      workshopsChecked: true,
      emailsReceived: [],
      subscribers: []
    };
  },
  mounted() {
    // Load Google Maps API script
    this.loadGoogleMapsScript();
  },
  methods: {
    submitForm() {
      if (this.message) {
        // Form for questions about workshops is submitted
        // Add data to emailsReceived array
        this.emailsReceived.push({
          name: this.name,
          email: this.email,
          message: this.message
        });
        console.log('Emails Received: ', this.emailsReceived);
      } else {
        // Form for subscription is submitted
        // Add data to subscribers array
        this.subscribers.push({
          name: this.name,
          email: this.email,
          newsletter: this.newsletterChecked,
          workshops: this.workshopsChecked
        });
        console.log('Subscribers:', this.subscribers);
      }

      // Clear form fields and checkboxes
      this.name = '';
      this.email = '';
      this.message = '';
      this.newsletterChecked = true;
      this.workshopsChecked = true;
    },
    loadGoogleMapsScript() {
      // Check if the Google Maps script is already loaded
      
      if (typeof google === 'undefined') {
        const script = document.createElement('script');
        script.defer = true;
        script.async = true;
        script.onload = this.initMap;
        document.head.appendChild(script);
      } else {
        // Google Maps script is already loaded, initialize the map
        this.initMap();
      }
    },
    initMap() {
      const position = { lat: -41.69140599172209, lng: 146.72657868289832 };
      const map = new google.maps.Map(document.getElementById('map'), {
        zoom: 7,
        center: position,
        mapId: 'DEMO_MAP_ID',
      });
      const marker = new google.maps.Marker({
        position: position,
        map: map,
        title: 'HiddenValley',
      });
    }
  }
}
</script>

<style scoped>
button,
input
{
  font-family: inherit;
  font-size: 100%;
}

.interest-form {
  position: relative;
  margin: 0 auto;
  padding: 0;
  box-sizing: border-box;
}

input {
  width: 150px;
  padding: 8px;
  margin: 0;
  margin-bottom: 12px;
  box-sizing: border-box;
}

.message-input {
  width: 100%;
  padding: 72px;
  margin: 0;
  margin-bottom: 12px;
  box-sizing: border-box;
}

fieldset {
    margin-bottom: 18px;
    width: 70%;
}

input[type="checkbox"] {
  appearance: none;
  position: relative;
  width: 1em;
  height: 1em;
  border: 1px solid gray;
  vertical-align: -12px;
  margin-left: 10px;
  margin-right: 6px;
  /* Green colour for customised checkmark */
  color: #28a745;
  padding: 0;
}

input[type="checkbox"]::before {
  /* Customised checkmark */
  content: "✔";
  position: absolute;
  font-size: 1.2em;
  right: -1px;
  top: -0.3em;
  /* Hiding checkmark when not checked */
  visibility: hidden;
}

input[type="checkbox"]:checked::before {
  /* Showing checkmark when checked */
  visibility: visible;
}
</style>
