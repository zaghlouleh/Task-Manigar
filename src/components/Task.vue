<template>
  <div 
    class="pr-3 h-6 rounded-full text-xs font-semibold flex items-center"
    :class="`text-white`"
  >
    <span class="rounded-full mr-1">
      <font-awesome-icon icon="comment" style="color: grey; " />
    </span>
    <span>
      <font-awesome-icon icon="paperclip" style="color: grey; " />
    </span>
    <span class="">
      <slot></slot>
    </span>
  </div>
</template>
<script>
export default {
  props: {
    color: {
      type: String,
      default: "teal",
    },
  },
};
</script>
<style scoped>

</style>