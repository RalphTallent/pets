<template>
  <div class="home-view-container">
    <h1>Adopt for new Application</h1>
    {{ getAllCats.length }}
    {{ animalsCount }}

    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group
        id="input-group-1"
        label="Pet's name:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="formatData.name"
          type="text"
          required
          placeholder="Enter pet's name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Species:" label-for="input-2">
        <b-form-select
          id="input-2"
          v-model="formatData.species"
          :options="['cats','dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        label="Pet's age:"
        label-for="input-3"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-3"
          v-model="formatData.age"
          type="number"
          required
          placeholder="Enter pet's age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>
<style scoped>
.btn {
  margin: 10px;
}
</style>
<script>
import { mapActions, mapGetters } from "vuex"

export default {
  name: "Home",
  data () {
    return {
      showPetForm: false,
      formatData: {
        name: "",
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      "animalsCount",
      "getAllCats"
    ])
  },
  methods: {
    ...mapActions([
      "addPet"
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formatData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      /* reset form after submit */
      this.formatData = {
        name: "",
        age: 0,
        species: null
      }
    }
  },
  components: ""
}
</script>
