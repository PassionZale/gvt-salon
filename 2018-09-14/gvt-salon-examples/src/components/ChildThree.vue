<template>
    <div style="margin-top:40px;">
      <div>
        <button class="btn btn-success" @click="click">{{ btnText }}</button>
        <p>子组件中的 count: {{ count }}</p>
      </div>
      <slot></slot>
    </div>
</template>

<script>
export default {
  name: "child-three",

  props: {
    msg: {
      type: String,
      default: "Child Default Msg"
    },
    btnText: {
      type: String,
      default: "Child Tree"
    },
    parentCount: {
      type: Number,
      default: 0
    }
  },

  data() {
    return {
      // 1. 将父组件传递的 parentCount 复制为子组件自身的 data
      count: this.parentCount
    };
  },

  watch: {
    /**
     * 2.
     * 观察父组件通过 props 传递的 parentCount
     * 若其发生改变, 则更新子组件自身的 count
     */
    parentCount(val){
      this.count = val;
    },

    /**
     * 3.
     * 观察子组件自身的 count
     * 若其发生改变, 则通过特殊的 update $emit, 通知父组件, 更新父组件自身的 count
     */
    count(val){
      this.$emit("update:parentCount", val);
    }
  },

  methods: {
    click() {
      console.log(this.msg);
      this.count ++;
    }
  }
};
</script>
