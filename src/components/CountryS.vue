<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select mb-10 mt-4 bg-blue-700 bg-opacity-40 w-full p-3 ronded shadow-lg"
  >
    <option value="0" class="">Select Country</option>
    <option v-for:="country in countries" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountryS",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);
      this.$emit("get-country", country);
    },
  },
};
</script>