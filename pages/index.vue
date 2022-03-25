<template>
  <main class="container my-5">
    <div class="row">
      <div class="col-12 my-3">
        <h3 class="mb-12">Lets get started list your place</h3>
      </div>
      <div class="col-12 my-3">
        <p class="mb-12"><small>Step 1</small></p>
      </div>
      <div class="col-12 my-3">
        <h3 class="mb-12">What kind of space do you have?</h3>
      </div>
      <div class="col-md-4">
        <form @submit.prevent="submitApartment">
            <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label for>Rooms</label>
                <select class="form-control" v-model="apartments.rooms">
                  <option value="room">Type of a room</option>
                  <option value="Private">Private</option>
                  <option value="Public">Public</option>
                  <option value="Executive">Executive</option>
                  <option value="Suite">Suite</option>
                  <option value="Presidential">Presidential</option>
                </select>
              </div>
            </div>
          </div>
          <div class="form-group">
            <label for>Number of guests</label>
            <input type="number" class="form-control" v-model="apartments.number_of_guests">
          </div>
          <div class="form-group">
            <label for>Location</label>
            <input type="text" class="form-control" v-model="apartments.location">
          </div>

          <button type="submit" class="btn btn-info">Continue</button>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      apartments: {
        rooms: "",
        number_of_guests: "",
        location: ""
      }
    };
  },

  methods: {
    async submitApartment() {
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.apartments) {
        formData.append(data, this.apartments[data]);
      }
      try {
        let response = await this.$axios.$post("/apartment/", formData, config);
        this.$router.push("/apartment/");
        console.log('=====', response)
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>
