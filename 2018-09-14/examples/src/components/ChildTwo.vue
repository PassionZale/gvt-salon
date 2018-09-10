<template>
    <button class="btn btn-danger" @click="click">Child Two</button>
</template>

<script>
import eventBus from "../utils";

export default {
  name: "child-two",

  data() {
    return {
      msg: "child-msg"
    };
  },

  mounted(){
    console.log(this.$attrs);
  },

  methods: {
    click(){
      eventBus.$emit("child-two-click", "child two say hi to child one");
    },
  }
};
</script>
