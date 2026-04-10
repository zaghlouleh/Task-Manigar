<template>
  <div class="px-3" style="border-radius: 14px">
    <div class="flex justify-between">
      <p class="text-black-700 font-semibold font-sans tracking-wide text-base">
        <font-awesome-icon
          style="color: rgb(72, 177, 219)"
          icon="align-justify"
        />
        Design Team Board
      </p>
    </div>
    <div class="flex flex-wrap -mx-3">
      <div class="md:w-1/3 px-3 md:mb-0">
        <div class="relative">
          <select
            style="border-radius: 12px"
            class="
              block
              appearance-none
              w-full
              bg-gray-200
              border border-gray-200
              text-black-700
              py-2
              px-4
              pr-8
              leading-tight
              focus:outline-none focus:bg-white focus:border-gray-500
            "
            v-model="tableNo"
          >
            <option v-for="table in tables" :key="table">{{ table }}</option>
          </select>
          <div
            class="
              pointer-events-none
              absolute
              inset-y-0
              right-0
              flex
              items-center
              px-2
              text-black-700
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
        </div>
      </div>
      <div class="md:w-1/3 px-3 mb-2 md:mb-0">
        <div class="relative">
          <select
            style="
              border-radius: 12px;
              background: rgba(216, 107, 17, 0.5);
              color: rgb(219, 107, 17);
            "
            class="
              block
              appearance-none
              w-full
              bg-gray-200
              border border-gray-200
              text-gray-700
              py-2
              px-4
              pr-8
              leading-tight
              focus:outline-none focus:bg-white focus:border-gray-500
            "
            v-model="tagName"
          >
            <option v-for="tag in tags" :key="tag">{{ tag }}</option>
          </select>
          <div
            class="
              pointer-events-none
              absolute
              inset-y-0
              right-0
              flex
              items-center
              px-2
              text-orange-700
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
        </div>
      </div>
    </div>
    <div class="flex flex-wrap ">
      <div class="w-full md:w-1/3  md:mb-0">
        <label style=" font-size: 25px;"
          class="
            block
            uppercase
            tracking-wide
            text-black-700 text-xs
            font-bold
          "
          for="grid-city"
          >Task :</label
        >
      </div>
      <div class="md:w-2/3 mt-2 md:mb-0 -mx-20">
        <input
          style="border-radius: 14px"
          class="
            appearance-none
            block
            w-full
            leading-tight
            focus:outline-none focus:bg-white focus:border-gray-500
          "
          type="text"
          v-model="taskName"
          @keyup.enter="addTask"
          placeholder="Enter Name"
          ref="taskname"
        />
      </div>
    </div>
    <div class="flex flex-wrap -mx-3">
      <div class="w-full px-3 mb-1 md:mb-0">
        <label
          class="
            block
            uppercase
            tracking-wide
            text-black-700 text-xs
            font-bold
            mb-1
          "
          for="grid-city"
          >members</label
        >
        <div class="col-md-2">
          <span class="mr-2 plus">
            <font-awesome-icon icon="plus" style="color: rgb(72, 177, 219)" />
          </span>
        </div>
        <div class="col-md-10" style="margin-top: 15px; position: relative">
          <b-img
            style="left: 70px; position: absolute"
            class="right"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            style="left: 90px; position: absolute"
            class="left"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            style="left: 110px; position: absolute"
            class="left"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            style="left: 130px; position: absolute"
            class="left"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
          <b-img
            class="left"
            src="../assets/3d1577bddc56e1f5366780934234b512.jpg"
            v-bind="mainProps"
            rounded="circle"
            alt="Circle image"
          ></b-img>
        </div>
      </div>
    </div>
    <div class="flex flex-wrap -mx-3">
      <div class="w-full px-3 mb-1 md:mb-0">
        <label
          class="
            block
            uppercase
            tracking-wide
            text-black-700 text-xs
            font-bold
            mb-1
          "
          for="grid-city"
          >Description</label
        >
        <input
          style="border-radius: 14px"
          class="
            appearance-none
            block
            w-full
            bg-gray-200
            text-gray-700
            border border-gray-200
            py-3
            px-4
            leading-tight
            focus:outline-none focus:bg-white focus:border-gray-500
          "
          type="text"
          v-model="taskDescription"
          @keyup.enter="addTask"
          placeholder="Enter Description"
          ref="taskdescription"
        />
      </div>
    </div>
    <label
      class="block uppercase tracking-wide text-black-700 text-xs font-bold"
      for="grid-state"
      >comments</label
    >
    <froala
      id="edit"
      :tag="'textarea'"
      :config="config"
      v-model="model"
    ></froala>
    <div class="flex flex-row-reverse items-center justify-between">
      <button
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-semibold
          py-2
          px-4
          mt-2
          rounded
          focus:outline-none focus:shadow-outline
        "
        type="button"
        @click="addTask"
      >
        Add
      </button>
    </div>
  </div>
</template>

<script>
// import VueFroala from 'vue-froala-wysiwyg';
export default {
  components: {},
  props: {
    tables: { type: Array },
  },
  data() {
    return {
      taskDescription: null,
      taskName: null,
      taskQty: 1,
      tableNo: "Backlog",
      tagName: "Medium",
      tags: ["Hige", "Low", "Medium"],

      mainProps: {
        blank: true,
        blankColor: "rgb(197, 197, 197)",
        width: 39,
        height: 39,
        class: "m1",
      },
      config: {},
      model: "Edit Your Content Here!",
    };
  },
  methods: {
    addTask: function () {
      this.$emit("addTask", {
        taskDescription: this.taskDescription,
        taskName: this.taskName,
        taskQty: this.taskQty,
        tableNo: this.tableNo,
        tagName: this.tagName,
      });
      this.taskName = "";
      this.taskDescription = "";
    },
  },
  mounted() {
    this.$refs.taskname.focus();
    this.$refs.taskdescription.focus();
  },
};
</script>

<style scoped>
.column-width {
  min-width: 280px;
  width: 280px;
}
.right {
  border: solid 2px rgb(255, 255, 255);
}
.left {
  float: left;
  cursor: pointer;
  border: solid 2px rgb(255, 255, 255);
}
.plus {
  border: dotted rgb(72, 177, 219);
  font-size: 15px;
  border-radius: 100%;
  padding: 8px 12px 8px 12px;
  margin-top: 5px;
  float: left;
  cursor: pointer;
}
</style>
