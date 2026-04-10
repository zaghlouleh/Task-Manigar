<template>
  <div class="container-fluid">
      <li class="mr-3 pluss left">
        <font-awesome-icon icon="house-user" />
      </li>
      <li class="mr-3 pluss left">
        <font-awesome-icon icon="calendar" />
      </li>
      <li >
      <search class="left" style="padding-top: 5px" />
      </li>
      <li class="right">
      <b-img
        style="margin: 2px 0 0 20px"
        v-bind="mainProps"
        rounded="circle"
        alt="Circle image"
      ></b-img>
      </li>
      <li class="mr-3 pluss right">
        <font-awesome-icon icon="bars" />
      </li>
      <li class="mr-3 pluss right d-none d-xl-block">
        <font-awesome-icon icon="question" />
      </li>
      <li class="mr-3 pluss right">
        <font-awesome-icon icon="bell" />
      </li>
      <li class="mr-3 plusss right" @click="showDash">
      <button><font-awesome-icon icon="plus" /></button>
      </li>
  </div>
</template>
<script>
import EventBus from "../eventBus";
import Search from "./Search.vue";
export default {
  components: { Search },
  data() {
    return {
      mainProps: {
        blank: true,
        blankColor: "rgb(72, 177, 219)",
        width: 40,
        height: 40,
        class: "m1",
      },
    };
  },
  methods:{
      showDash: function () {
      EventBus.$emit("showDash");
    },
  }
};
</script>
<style scoped>
/* body {
  width: 100%;
} */
.pluss {
  border: solid 2px rgb(72, 177, 219);
  font-size: 15px;
  border-radius: 25%;
  padding: 8px 11px 8px 11px;
  cursor: pointer;
  color: rgb(72, 177, 219);
}
.plusss {
  border: solid 2px rgb(72, 177, 219);
  font-size: 15px;
  border-radius: 25%;
  padding: 8px 11px 8px 11px;
  cursor: pointer;
  background: rgb(72, 177, 219);
  color: white;
}
.left {
  float: left;
}
.right {
  float: right;
}

</style>