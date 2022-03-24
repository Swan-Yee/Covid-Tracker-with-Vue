<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold"> New: </span>
        {{ numberWithCommas(status.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold"> Total: </span>
        {{ numberWithCommas(status.TotalConfirmed) }}
      </div>
    </div>
    <div class="shadow bg-blue-200 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Death</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold"> New: </span>
        {{ numberWithCommas(status.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold"> Total: </span>
        {{ numberWithCommas(status.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["status"],
  methods: {
    numberWithCommas(x) {
      return x.toString().replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1,");
    },
  },
};
</script>

<style></style>
