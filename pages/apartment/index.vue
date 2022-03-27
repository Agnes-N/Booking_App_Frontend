<script>
import Vue from 'vue'
import vueCountryRegionSelect from 'vue-country-region-select'

Vue.use(vueCountryRegionSelect)

export default {
  data() {
    return {
      locations: {
        country: "",
        street_address: "",
        access_code: ""
      }
    };
  },
  methods: {
    async submitLocation() {
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.locations) {
        formData.append(data, this.locations[data]);
      }
      try {
        let response = await this.$axios.$post("/location/", formData, config);
        this.$router.push("/amnesity/amnesity/");
        console.log('=====', response)
      } catch (e) {
        console.log(e);
      }
    },

    async back() {
      try {
        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<template>
  <main class="container my-5">
    <div>
      <h4>Where is your place located?</h4>
      <p>Guests will only get your exact address once they have booked a reservation.</p>
    </div>
    <div>
      <button type="button" class="btn btn-outline-info">Use current location</button>
    </div>
    <div>
      <p><small>---------or enter your address---------</small></p>
    </div>
    <form>
      <div class="row">
      <div class="col-md-6">
        <div class="form-group">
          <label for>Country/ Region</label>
          <country-select v-model="locations.country" class="form-control" />
        </div>
      </div>
    </div>
    <div class="form-group">
      <label for>Street address</label>
      <input type="text" class="form-control" v-model="locations.street_address">
    </div>
    <div class="form-group">
      <label for>Apt.Suite (Optional)</label>
      <input type="text" class="form-control" v-model="locations.access_code">
    </div>
      <div class="row">
        <div class="col">
          <button @click.prevent="back" type="submit" class="btn btn-info">Back</button>
        </div>
        <div class="col">
          
        </div>
        <div class="col">
          <button @click.prevent="submitLocation" type="submit" class="btn btn-info">Next</button>
        </div>
      </div>
    </form>
    <form></form>
  </main>
</template>
