<template>
  <div>
    <div class="hearder" id="divMove"  :style="styleString" ref="eleMove" @mousedown="down" @touchstart="down">
       <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name:'moveFunc',
  props:{
    styleString:{
      type: String,
      default: "bottom: 8rem; right: 1rem;"
    },
    movePositon:{
      type: String,
      default: ""
    },

  },
  data() {
    return {
      flags: false,
      maxW: "",
      maxH: "",
      oL: "",
      oT: ""
    };
  },
  mounted() {
    console.log(this.movePositon)
    // this.nodeEle = document.getElementById("divMove");
    this.nodeEle = this.$refs.eleMove;
    this.maxW = document.documentElement.clientWidth - this.nodeEle.offsetWidth;
    this.maxH = document.documentElement.clientHeight - this.nodeEle.offsetHeight;
    console.log(this.nodeEle.offsetWidth)

  },
  methods: {
    down(e) {
      this.flags = true;
      var event = e || window.event;
      var touch = event.touches ? event.touches[0] : event;
      this.oL = touch.clientX - this.nodeEle.offsetLeft;
      this.oT = touch.clientY - this.nodeEle.offsetTop;
      document.addEventListener("touchmove", this.move, false);
      document.addEventListener("mousemove", this.move, false);
      document.addEventListener("mouseup", this.end, false);
      document.addEventListener("touchend", this.end, false);
    },
    move(e) {
      if (this.flags) {
        var event = e || window.event;
        var touch = event.touches ? event.touches[0] : event;
        var oLeft = touch.clientX - this.oL;
        var oTop = touch.clientY - this.oT;
        //范围限定优化方法
        oLeft = Math.min(this.maxW, Math.max(0, oLeft));
        oTop = Math.min(this.maxH, Math.max(0, oTop));
        // if (oLeft < 0) {
        //   oLeft = 0;
        // } else if (oLeft >= this.maxW) {
        //   oLeft = this.maxW;
        // }
        // if (oTop < 0) {
        //   oTop = 0;
        // } else if (oTop >= this.maxH) {
        //   oTop = this.maxH;
        // }
        if(this.movePositon == "moveX"){
          this.nodeEle.style.left = oLeft+"px";
          this.nodeEle.style.right = "auto";
        }else if(this.movePositon == "moveY"){
           this.nodeEle.style.top = oTop+"px";
           this.nodeEle.style.bottom = "auto";
        }else{
          this.nodeEle.style.left = oLeft+"px";
          this.nodeEle.style.right = "auto";
          this.nodeEle.style.top = oTop+"px";
          this.nodeEle.style.bottom = "auto";
        }

      }
    },
    //鼠标释放时候的函数
    end() {
      this.flags = false;
      document.removeEventListener("touchmove", this.move, false);
      document.removeEventListener("mousemove", this.move, false);
      document.removeEventListener("mouseup", this.move, false);
      document.removeEventListener("touchend", this.move, false);
    }
  }
};
</script>
<style scoped>
.hearder {
  position: fixed!important;
  z-index: 2019;
  touch-action: none;
}

</style>