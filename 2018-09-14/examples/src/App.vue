<template>
  <div class="container" style="margin-top: 40px;">

    <!-- $refs, $children, $parent 父子组件通讯 -->
    <child-one ref="child-one" @on-click="childClickHandler"></child-one>

    <!-- eventBus 兄弟组件 or 祖孙组件通讯 -->
    <child-two :data-abc="mock"></child-two>

    <!-- props 父子组件通讯 -->
    <!--msg: 静态传值-->
    <!--btnText: 动态传值-->
    <!--parentCount: 双向绑定-->
    <child-three msg="msg-from-parent" :btn-text="btnText" :parent-count.sync="count">
      <div>
        <button class="btn btn-default" @click="() => count++">Parent Button</button>
        <p>父组件中的 count: {{count}}</p>
      </div>
    </child-three>

  </div>
</template>

<script>
import ChildOne from "./components/ChildOne.vue";
import ChildTwo from "./components/ChildTwo.vue";
import ChildThree from "./components/ChildThree.vue";

export default {
  name: "app",

  components: { ChildOne, ChildTwo, ChildThree },

  data() {
    return {
      mock: "parent mock data",
      msg: "parent-msg",
      btnText: "Parent Changed me",
      count: 0
    };
  },

  mounted() {
    // 访问整个子组件实例
    const ref_childInstance = this.$refs["child-one"];
    const children_childInstance = this.$children[0];

    // 访问子组件名称
    const ref_name = this.$refs["child-one"].$options.name;
    const children_name = this.$children[0].$options.name;

    // 访问子组件 data attributes
    const ref_msg = this.$refs["child-one"]["msg"];
    const children_msg = this.$children[0]["msg"];

    // 访问子组件 methods
    this.$refs["child-one"].child_func();
    this.$children[0].child_func();
  },

  methods: {
    // 父组件通过事件监听子组件的传值
    childClickHandler(msg_form_child_one) {
      alert(msg_form_child_one);
    }
  }
};
</script>