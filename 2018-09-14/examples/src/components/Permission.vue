<template>
  <div>
    <button type="button" class="btn btn-warning" v-permission="1">权限按钮一</button>
    <button type="button" class="btn btn-warning">权限按钮二</button>
  </div>
</template>

<script>

const hasPermission = (val) => {
    return false;
}

export default {
  directives: {
    permission: (el, binding, vnode) => {
      if (!hasPermission(binding.value)) {
        // replace HTMLElement with comment node
        const comment = document.createComment(" ");
        Object.defineProperty(comment, "setAttribute", {
          value: () => undefined
        });
        vnode.elm = comment;
        vnode.text = " ";
        vnode.isComment = true;
        vnode.context = undefined;
        vnode.tag = undefined;
        vnode.data.directives = undefined;

        if (vnode.componentInstance) {
          vnode.componentInstance.$el = comment;
        }

        if (el.parentNode) {
          el.parentNode.replaceChild(comment, el);
        }
      }
    }
  },

  methods: {
      hasPermission(){
        return false;
      }
  }
};
</script>
