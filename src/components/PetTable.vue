<template>
  <div>
    <h1>{{ species }} for Application</h1>
    <b-table striped hover :items="pets">
      <template #cell(name)="data">
        <router-link :to="`/pet/${species}/${data.index}`">{{ data.value }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
export default {
  name: "PetTable",
  props: {
    species: String,
    pets: Array
  }
}
</script>

<style scoped>

</style>
