<template>
  <div class="main">
    <div class="main-container">
      <div class="main-heading">
        <h1>Hidden Valley</h1>
        <h2>Gift Vouchers</h2>
        </div>
        <div class="main-other">
        <div class="main-left">
          <PremiumWorkshops />
        </div>
        <div class="main-right">
          <ul class="main-text">
            <li class="main-li">Give an experience as a gift and buy a gift voucher to either our standard or premium workshops.</li>
            <div class="booking-container">
                <div class="booking">
                  <div class="booking-left">
                    <div class="booking-text">Premium Voucher</div>
                  </div>
                  <button class="button button2" @click="redirectToExternalLink">Buy Now</button>
                </div>
              </div>
              <div class="booking-container">
                <div class="booking">
                  <div class="booking-left">
                    <div class="booking-text">Standard Voucher</div>
                  </div>
                  <button class="button button2" @click="redirectToExternalLink">Buy Now</button>
                </div>
              </div>

            <li class="main-li">Buy gift vouchers for 2 standard workshops and 1 premium workshop for the special price of $300:</li>
            <div class="booking-container">
                <div class="booking">
                  <div class="booking-left">
                    <div class="booking-text">Special</div>
                  </div>
                  <button class="button button2" @click="redirectToExternalLink">Buy Now</button>
                </div>
              </div>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import PremiumWorkshops from '../components/PremiumWorkshops.vue'
 export default {
  components: {
    PremiumWorkshops // Register the PremiumWorkshop component
  },
  data() {
    return {
    };
  },
  methods: {
    redirectToExternalLink() {
        window.location.href = 'https://www.eventbrite.com.au/d/australia--tasmania/events/';
    }
  },
}
</script>