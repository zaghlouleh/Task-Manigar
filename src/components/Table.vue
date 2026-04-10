<template>
  <div
    class="bg-gray-200 rounded-lg px-2 py-2 mb-5 column-width  mr-4"
    id="table2" style="border-radius: 14px"
  >
    <div class="flex justify-between">
      <p
        class="text-gray-700 font-semibold font-sans mt-2 tracking-wide text-sm">{{ column.title }}
      </p>
      <p
        class="text-gray-700 font-semibold font-sans mt-2 shadow tracking-wide text-xs btnnn">{{ totalItem }}
      </p>
      <button
        class=" mb-2 font-semibold font-sans tracking-wide btnn"
        @click="showTask">+
      </button>
    </div>
    <div class="flex h-screen pb-10 overflow-auto">
      <draggable
        :list="column.tasks"
        :animation="200"
        ghost-class="ghost-card"
        group="tasks"
        handle=".handle"
        class="items-stretch w-full "
      >
        <!-- Each element from here will be draggable and animated. Note :key is very important here to be unique both for draggable and animations to be smooth & consistent. -->
        <task-card
          v-for="task in column.tasks"
          :key="task.id"
          :task="task"
          class="mt-3"
        ></task-card>
      </draggable>
    </div>
  </div>
</template>

<script>
import EventBus from "../eventBus";
import draggable from "vuedraggable";
import taskCard from "./TaskCard.vue";

export default {
  components: {
    taskCard,
    draggable,
  },
  props: {
    column: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {};
  },
  methods: {
    showTask: function () {
      EventBus.$emit("showTask");
    },
  },
  computed: {
    totalItem: function () {
      let sum = 0;
      this.column.tasks.forEach(function (person) {
        sum += person.task;
      });

      return sum;
    },
  },
};
</script>

<style>
.column-width {
  min-width: 290px;
  width: 290px;
}
/* Unfortunately @apply cannot be setup in codesandbox, 
but you'd use "@apply border opacity-50 border-blue-500 bg-gray-200" here */
.ghost-card {
  opacity: 0.5;
  background: #f7fafc;
  border: 1px solid #4299e1;
  /* margin-bottom: 10px; */
}
.btnnn {
  display: inline-block;
  padding:0 14px 0 14px;
  margin-right: 100px;
  background: white;
  border: 2px white;
  border-radius: 10px;
  font-size: 15px;
}
.btnn {
  display: inline-block;
  padding:0 14px 0 14px;
  border-radius: 10px;
  font-size: 20px;
  cursor: pointer;
  color: rgb(158, 158, 158);
}
.btnn:hover {
  color: rgb(72, 177, 219);
}
.btnnn:hover {
  background-color: rgba(72, 177, 219, .3);
  color: rgb(72, 177, 219);
}
</style>
