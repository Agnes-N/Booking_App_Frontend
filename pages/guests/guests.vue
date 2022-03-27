<template>
  <main class="container my-5">
    <div>
      <h3 class="mb-12">How many can your place accommodate?</h3>
        <p>Check that you have enough beds to accommodate all your guests comfortably.</p>
    </div>
    <div>
    <form>
      <div>
        <label for="sb-inline">Guests</label>
        <b-form-spinbutton v-model="guest.guests" id="sb-inline" inline></b-form-spinbutton>
      </div>
      <div>
        <label for>How many bedrooms can guests use?</label>
        <select class="form-control" v-model="guest.bedrooms">
          <option value="bedroom">Select bredroom type</option>
          <option value="Studio">Studio</option>
          <option value="Ordinary">Ordinary</option>
          <option value="Officetel">Officetel</option>
          <option value="Penthouse">Penthouse</option>
        </select>
      </div>
      <div>
        <label for="sb-inline">Beds</label>
        <b-form-spinbutton v-model="guest.beds" id="sb-inline" inline></b-form-spinbutton>
      </div>

      <div class="row">
        <div class="col">
          <button @click.prevent="back" type="submit" class="btn btn-info">Back</button>
        </div>
        <div class="col">

        </div>
        <div class="col">
          <button @click.prevent="submitGuests" type="submit" class="btn btn-info">Submit</button>
        </div>
      </div>
    </form>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      guest: {
        guests: "",
        bedrooms: "",
        beds: ""
      }
    };
  },
  methods: {
    async back() {
      try {
        this.$router.push("/amnesity/amnesity/");
      } catch (e) {
        console.log(e);
      }
    },

    async submitGuests() {
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.guest) {
        formData.append(data, this.guest[data]);
      }
      try {
        let response = await this.$axios.$post("/guest/", formData, config);
        this.$router.push("/");
        console.log('=====', response)
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>
