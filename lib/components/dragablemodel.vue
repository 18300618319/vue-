<template>
    <div class="alert" v-show="model1" @mouseup="mouseup" @mousemove="mousemove">
      <div id="dragdiv" class="divblok" @mouseup="mouseup" :style="'left:'+left+'px;top:'+top+'px;'">
        
          <p class="lh_kx" style="text-align:center" @mousedown="mousedown">
            <slot name="top"></slot>
          </p>
        <div class="icon_gb" @click="close"><Icon type="close" size='25' style="z-index:100"/></div>
        <slot name="main">
         
        </slot> 
      </div>
    </div>
</template>

<script>
export default {
  name: "dragablemodel",
  props: {
    model: Boolean,
    value: Boolean
  },
  data() {
    return {
      left: 700,
      top: 200,
      x: 0,
      y: 0,
      down: false,
      model1: false
    };
  },
  watch: {
    value(data) {
      this.model1 = this.value;
    }
  },
  methods: {
    mousedown(e) {
      console.log(e, "rrrrrrrrr");
      this.down = true;
      this.x = e.x;
      this.y = e.y;
    },
    mousemove(e) {
      if (this.down) {
        if (this.left > 200 && this.left < this.innerWidth - 620) {
          this.left += e.x - this.x;
        }
        if (this.left <= 200 && e.x - this.x > 0) {
          this.left += e.x - this.x;
        }
        if (this.left >= this.innerWidth - 620 && e.x - this.x < 0) {
          this.left += e.x - this.x;
        }

        if (this.top > 100 && this.top < this.innerHeight - 420) {
          this.top += e.y - this.y;
        }
        if (this.top <= 100 && e.y - this.y > 0) {
          this.top += e.y - this.y;
        }
        if (this.top >= this.innerHeight - 420 && e.y - this.y < 0) {
          this.top += e.y - this.y;
        }
        this.x = e.x;
        this.y = e.y;
      }
    },
    mouseup(e) {
      this.down = false;
    },
    mouseout(e) {
      this.down = false;
    },
    close() {
      console.log("uuuuuuuuuuuuuu");
      this.model1 = false;
      this.$emit("input", false);
      this.$emit("on-cancel");
    }
  },
  mounted() {
    this.model1 = this.value;
    this.innerHeight = window.innerHeight;
    this.innerWidth = window.innerWidth;

    window.onresize = function(e) {
      this.innerHeight = window.clientHeight;
      this.innerWidth = document.body.clientWidth;
    };
  }
};
</script>

<style>
.lh_kx {
  font-size: 18px;
  padding: 10px 0;
  background-color: #f1f1f1;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border-radius: 5px 5px 0 0;
}
.icon_gb {
  position: absolute;
  right: 20px;
  top: 10px;
  cursor: pointer;
}
.alert {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: 1000;
}
.divblok {
  background-color: #fff;
  position: fixed;
  left: 30%;
  top: 20%;
  width: 600px;
  border-radius: 5px;
}
</style>
