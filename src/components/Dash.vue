<template>
  <div
    class="bg-gray-200 rounded-lg px-2 py-2 mb-5 column-width overflow-auto  mr-4"
    id="table2" style="border-radius: 14px"
  >
    <div class="flex justify-between">
      <p
        class="text-gray-700 font-semibold font-sans mt-2 tracking-wide text-sm">{{ dash.title }}
      </p>
      <p
        class="text-gray-700 font-semibold font-sans mt-2 shadow tracking-wide text-xs btnnn">{{ totalDash }}
      </p>
    </div>
 </div>
</template>

<script>

export default {
  components: {},
  props: {
    dash: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {};
  },
  computed: {
    totalDash: function () {
      let sum = 0;
      this.dash.columns.forEach(function (person) {
        sum += person.column;
      });

      return sum;
    },
  },
};
</script>
