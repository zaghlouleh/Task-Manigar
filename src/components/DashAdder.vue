<template>
  <div class="px-3 py-3 rounded w-full">
    <div class="flex justify-between mb-4">
      <p class="text-gray-700 font-semibold font-sans tracking-wide text-base">Add new dash</p>
    </div>
    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full px-3 mb-4 md:mb-0">
        <label
          class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
          for="grid-city"
        >Full Name Dash</label>
        <input
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          type="text"
          placeholder="enter dash name"
          v-model="dashName"
          @keyup.enter="addDash"
          ref="dashname"
        >
      </div>
    </div>
    <div class="flex flex-row-reverse items-center justify-between">
      <button
        class="bg-blue-500 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="button"
        @click="addDash"
      >Add</button>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      dashName: null
    };
  },
  methods: {
    addDash: function () {
      this.$emit("addDash", this.dashName);
      this.dashName = "";
    },
  },
  mounted() {
    this.$refs.dashname.focus();
  },
};
</script>

<style scoped>
.column-width {
  min-width: 100%;
  width: 100%;
}

</style>
