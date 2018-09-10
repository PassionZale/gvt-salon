<template>
    <button class="btn btn-primary" @click="click">Child One</button>
</template>

<script>
import eventBus from "../utils";

export default {
  name: "child-one",

  data() {
    return {
      msg: "child-msg"
    };
  },

  mounted(){
    eventBus.$on('child-two-click', this.childTwoClickHandler);
  },

  methods: {
    child_func() {
      console.log("child-func");
    },

    click(){
        const param = "child one say hi to parent";
        // 子组件通过事件向父组件传值
        this.$emit('on-click', param);
    },

    childTwoClickHandler(msg_from_child_two){
      alert(msg_from_child_two)
    },
  }
};
</script>
