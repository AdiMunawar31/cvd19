<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-lg bg-yellow-300 p-10 text-center rounded bg-opacity-20">
      <h3 class="text-3xl text-blue-100 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold"> New: </span>
        {{ numComma(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold"> Total: </span>
        {{ numComma(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- Box 2 -->
    <div class="shadow-lg bg-red-400 p-10 text-center rounded bg-opacity-25">
      <h3 class="text-3xl text-blue-100 font-bold mb-4">Deaths</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold"> New: </span>
        {{ numComma(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold"> Total: </span>
        {{ numComma(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    numComma(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>