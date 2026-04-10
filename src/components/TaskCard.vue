<template>
  <div
    class="bg-gray-200 handle cursor-move bg-white shadow px-3 pt-2 pb-2 border border-white"
    style="border-radius: 14px; background: white"
  >
    <div class="flex flex-row">
      <div class="flex-grow pr-1">
        <div class="flex justify-between">
          <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">
            {{ task.title }}
          </p>
        </div>
        <div class="flex justify-between">
          <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">
            {{ task.Description }}
          </p>
        </div>
        <div class="flex justify-between">
          <div class="flex mt-1 items-center">
            <task v-if="task.task" :color="badgeColor">{{ task.task }}</task>
            <button
              style="padding-bottom: 10px"
              alt="remove task card"
              class="flex justify-between items-center text-center text-sm border-red-200 rounded px-2 py-1 hover:border-red-500 hover:bg-red-200 h-6 w-auto"
              @click="removeTask"
            >
              <font-awesome-icon icon="trash" size="xs" style="color: Tomato" />
            </button>
            <span :color="badgeColor" style="padding-left: 70px">
              <badge v-if="task.type" :color="badgeColor">{{ task.type }}</badge>
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import EventBus from "../eventBus";
import Badge from "./Badge.vue";
import Task from "./Task.vue";

export default {
  components: {
    Badge,
    Task,
  },
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
    count: {
      type: String,
    },
  },
  methods: {
    removeTask() {
      var r = confirm("Please confirm to remove!");
      if (r === true) {
        EventBus.$emit("removeTask", {
          taskName: this.task.title,
          taskDescription: this.task.Description,
          taskId: this.task.id,
        });
      }
    },
  },
  computed: {
    badgeColor() {
      const mappings = {
        Hige: "red",
        Low: "teal",
        Medium: "orange",
      };
      return mappings[this.task.type] || "teal";
    },
  },
};
</script>

<style scoped></style>
