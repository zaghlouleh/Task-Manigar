<template>
  <div id="app">
    <div class="flex flex-col">
      <nav class="pt-1 mt-0 fixed li z-10 border col-md-12">
        <!-- <div class="container mx-auto  flex-wrap items-center"> -->
        <nav-bar />

        <vue-tailwind-modal
          :showing="showTaskModal"
          @close="showTaskModal = false"
        >
          <task-adder v-on:addTask="addTaskEvent" :tables="tables"></task-adder>
        </vue-tailwind-modal>
        <vue-tailwind-modal
          :showing="showTableModal"
          @close="showTableModal = false"
        >
          <table-adder v-on:addTable="addTableEvent"></table-adder>
        </vue-tailwind-modal>
        <vue-tailwind-modal
          :showing="showDashModal"
          @close="showDashModal = false"
        >
          <dash-adder v-on:addDash="addDashEvent"></dash-adder>
        </vue-tailwind-modal>
        <!-- </div> -->
      </nav>
    </div>
    <vueper-slides
      bullets-inside
      transition-speed="250"
      :arrows="false"
      :slide-ratio="2 / 3"
      :infinite="false"
      :touchable="false"
    >
      <div class="container-fluid li fixed">
        <li class="left">
          <h1>Design Team Board</h1>
        </li>
        <li class="right" style="margin-top: 17px">
          <button
            class="inline-block text-gray-200 no-underline w-100 px-10 py-1"
            @click="clearAll"
            style="border-radius: 10px; background: rgb(72, 177, 219)"
          >
            Reset
            <div
              style="padding-top: 10px"
              class="
                pointer-events-none
                absolute
                inset-y-0
                right-0
                flex
                items-center
                px-3
                text-white-700
              "
            >
              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                ></path>
              </svg>
            </div>
          </button>
        </li>
        <li class="right" style="margin: 17px 17px 0 17px; position: relative">
          <b-img
            style="right: 20px; position: absolute"
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            style="right: 40px; position: absolute"
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            style="right: 60px; position: absolute"
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <p class="num" style="right: 62px">MH</p>
          <b-img
            style="right: 80px; position: absolute"
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <p class="num" style="right: 3px">+16</p>
        </li>
        <li class="right" style="padding-right: 70px">
          <h5 style="margin-top: 20px">Add member</h5>
        </li>
        <li class="right">
          <span class="mr-1 plus">
            <font-awesome-icon
              icon="plus"
              style="color: rgb(72, 177, 219); margin-top: 29px"
            />
          </span>
        </li>
      </div>
      <div
        class="container-fluid min-h-screen justify-center mx-auto"
        style="padding-top: 150px"
      >
        <div class="flex pt-180 overflow-auto">
          <div class="inserters"></div>
          <task-table
            v-for="column in columns"
            :key="column.title"
            :column="column"
          ></task-table>
          <button
            class="
              text-gray-700
              font-semibold font-sans
              tracking-wide
              text-xs
              btnn
              button
            "
            @click="showTableModal = true"
          >
            +
          </button>
        </div>
      </div>
      <vueper-slide v-for="i in 4" :key="i" />
    </vueper-slides>
  </div>
</template>

<script>
import { VueperSlides, VueperSlide } from "vueperslides";
import "vueperslides/dist/vueperslides.css";
import VueTailwindModal from "vue-tailwind-modal";
import uuid from "uuid-random";
import EventBus from "./eventBus";
import tasklist from "./tasklist.js";
import TaskTable from "./components/Table.vue";
import TableAdder from "./components/TableAdder.vue";
import TaskAdder from "./components/TaskAdder.vue";
import NavBar from "./components/NavBar.vue";
import DashAdder from "./components/DashAdder.vue";
export default {
  name: "App",
  components: {
    VueperSlides,
    VueperSlide,
    VueTailwindModal,
    TaskTable,
    TableAdder,
    TaskAdder,
    NavBar,
    DashAdder,
  },
  created() {
    EventBus.$on("removeTask", this.removeTaskEvent);
    EventBus.$on("showTask", this.addTaskEvent);
    EventBus.$on("showDash", this.addDashEvent);
  },
  beforeDestroy() {
    EventBus.$off("removeTask", this.removeTaskEvent);
    EventBus.$off("showTask", this.addTaskEvent);
    EventBus.$off("showDash", this.addDashEvent);
  },
  data() {
    return {
      showDashModal: false,
      showTaskModal: false,
      showTableModal: false,
      dashes: [],
      columns: tasklist,
      mainProps: {
        blank: true,
        blankColor: "rgb(197, 197, 197)",
        width: 39,
        height: 39,
        class: "m1",
      },
    };
  },
  methods: {
    addTableEvent(value) {
      this.columns.push({
        title: value,
        tasks: [],
      });
      this.showTableModal = false;
    },
    addDashEvent(value) {
      this.showDashModal = true;
      this.dashes.push({
        title: value,
        columns: [],
      });
      this.showDashModal = false;
    },
    addTaskEvent(value) {
      this.showTaskModal = true;
      for (var i = 0; i < this.columns.length; i++) {
        if (this.columns[i].title === value.tableNo) {
          this.columns[i].tasks.push({
            id: uuid(),
            title: value.taskName,
            Description: value.taskDescription,
            type: value.tagName,
            task: parseInt(value.taskQty),
          });
        }
      }
      this.showTaskModal = false;
    },
    removeTaskEvent(value) {
      for (var i = 0; i < this.columns.length; i++) {
        for (var k = 0; k < this.columns[i].tasks.length; k++) {
          if (this.columns[i].tasks[k].id === value.taskId) {
            this.columns[i].tasks.splice(k, 1);
          }
        }
      }
    },
    clearAll() {
      var r = confirm("Please confirm to remove all tasks!");
      if (r === true) {
        this.columns = [];
        this.columns.push({
          title: "Backlog",
          tasks: [],
        });
      }
    },
  },
  computed: {
    tables: function () {
      let array = [];
      this.columns.forEach(function (item) {
        array.push(item.title);
      });
      return array;
    },
  },
  watch: {
    showTaskModal: function (newValue) {
      if (newValue === true) {
        this.showTableModal = false;
        this.showDashModal = false;
      }
    },
    showDashModal: function (newValue) {
      if (newValue === true) {
        this.showTaskModal = false;
        this.showTableModal = false;
      }
    },
    showTableModal: function (newValue) {
      if (newValue === true) {
        this.showTaskModal = false;
        this.showDashModal = false;
      }
    },
    columns: {
      handler(value) {
        localStorage.tasks = JSON.stringify(value);
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      this.columns = JSON.parse(localStorage.getItem("tasks"));
    }
  },
};
</script>

<style >
/* .vueperslides__bullet .default {
  background-color: rgba(0, 0, 0, 0.3);
  border: none;
  box-shadow: none;
  transition: 0.3s;
  width: 16px;
  height: 16px;
}

.vueperslides__bullet--active .default {background-color: #42b983;}

.vueperslides__bullet span {
  display: block;
  color: #fff;
  font-size: 10px;
  opacity: 0.8;
} */
.button {
  height: 30px;
  background: rgb(72, 177, 219);
  color: white;
}
.button:hover {
  background: rgba(72, 177, 219, 0.5);
  color: rgb(72, 177, 219);
}
.dmv-text-xs {
  font-size: 0.75rem;
}
.num {
  position: absolute;
  color: white;
  font-size: 11px;
  margin-top: 11px;
}
.right {
  float: right;
  cursor: pointer;
  border: solid 2px rgb(255, 255, 255);
}
.left {
  float: left;
  cursor: pointer;
  border: solid 2px rgb(255, 255, 255);
}

.plus {
  border: dotted 2px rgb(72, 177, 219);
  font-size: 15px;
  border-radius: 100%;
  padding: 9px 11px 9px 11px;
  cursor: pointer;
}
.vueperslides__bullets {
  margin-bottom: 3px;
}
.vueperslides__bullet .default {
  background-color: rgba(0, 0, 0, 0.3);
  border: none;
  box-shadow: none;
  transition: 0.3s;
  width: 20px;
  height: 20px;
}
.vueperslides__bullet--active .default {
  background-color: rgb(72, 177, 219);
}

.vueperslides__bullet span {
  display: block;
  color: #fff;
  font-size: 10px;
  opacity: 0.8;
}
.li {
  background: white;
  margin-top: 63px;
  list-style-type: none;
  text-decoration: none;
}
</style>
