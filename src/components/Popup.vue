
<script>
// # template version
// <template>
//   <div class="mask">
//     <div class="popup">
//       <h1>{{ title }}</h1>
//       <slot v-if="$scopedSlots.default()" :child-prop="$attrs">
//         default slot
//       </slot>
//       <p v-else>{{ content }}</p>
//       <button @click="$emit('on-confirm', childData)">confrim</button>
//       <button @click="$emit('on-cancel')">cancel</button>
//     </div>
//   </div>
// </template>
export default {
  data() {
    return {
      childData: "childData",
    };
  },
  props: ["title", "content"],
  render(h) {
    console.log("this.$scopedSlots---", this.$scopedSlots);

    return h("div", { class: "mask" }, [
      h("div", { class: "popup" }, [
        h("h1", this.title),
        this.$scopedSlots.default()
          ? this.$scopedSlots.default(this.$attrs)
          : h("p", this.content),
        h(
          "button",
          {
            on: {
              click: () => {
                this.$emit("on-confirm", this.childData);
              },
            },
          },
          "confrim"
        ),
        h(
          "button",
          {
            on: {
              click: () => {
                this.$emit("on-cancel");
              },
            },
          },
          "cancel"
        ),
      ]),
    ]);
  },
};
</script>

<style>
.mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background:#000000c7;
}
.popup {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  height: 300px;
  background: #f27777;
  z-index: 9999999;
}
</style>