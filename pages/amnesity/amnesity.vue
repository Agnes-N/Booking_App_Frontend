<template>
  <main class="container my-5">
    <div>
      <h3 class="mb-12">What amnesities</h3>
        <p>These are just the amnesities guests usually except, but can add even more after you publish</p>
    </div>
    <div>
    <form>
        <div class="form-check">
            <div class="row">
                <div class="col">
                    <label class="form-check-label" for="exampleRadios1">
                    Essentials
                    </label>
                </div>
                <div class="col"></div>
                <div class="col">
                    <input v-model="amnesity.amneties" class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios1" value="Essentials">
                </div>
            </div>
        </div>
        <hr>
        <div class="form-check">
            <div class="row">
                <div class="col">
                    <label class="form-check-label" for="exampleRadios2">
                    Wifi
                    </label>
                </div>
                <div class="col"></div>
                <div class="col">
                    <input v-model="amnesity.amneties" class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios2" value="Wifi">
                </div>
            </div>
        </div>
        <hr>
        <div class="form-check">
            <div class="row">
                <div class="col">
                    <label class="form-check-label" for="exampleRadios3">
                    TV
                    </label>
                </div>
                <div class="col"></div>
                <div class="col">
                    <input v-model="amnesity.amneties" class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios3" value="TV">
                </div>
            </div>
        </div>
        <hr>
        <div class="form-check">
            <div class="row">
                <div class="col">
                    <label class="form-check-label" for="exampleRadios4">
                    Heat
                    </label>
                </div>
                <div class="col"></div>
                <div class="col">
                    <input v-model="amnesity.amneties" class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios4" value="Heat">
                </div>
            </div>
        </div>
        <hr>

      <div class="row">
        <div class="col">
          <button @click.prevent="back" type="submit" class="btn btn-info">Back</button>
        </div>
        <div class="col">

        </div>
        <div class="col">
          <button @click.prevent="submitAmnesity" type="submit" class="btn btn-info">Next</button>
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
      amnesity: {
        amneties: ""
      }
    };
  },
  methods: {
    async submitAmnesity() {
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.amnesity) {
        formData.append(data, this.amnesity[data]);
      }
      try {
        let response = await this.$axios.$post("/amnesity/", formData, config);
        this.$router.push("/guests/guests/");
        console.log('=====', response)
      } catch (e) {
        console.log(e);
      }
    },

    async back() {
      try {
        this.$router.push("/amnesity/amnesity/");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>
