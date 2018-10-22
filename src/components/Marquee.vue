<template>
  <div :class="'marquee-wrapper '+className" ref="wrapper">
    <div class="marquee-list" ref="ListRef1">
      <span
        v-for="(item, index) in list"
        :key="index">
        {{item}}
      </span>
    </div>
    <div class="marquee-list" ref="ListRef2">
      <span
        v-for="(item, index) in list"
        :key="index">
        {{item}}
      </span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'vue-marquee-lite',
  data() {
    return {
      list: [],
      timer: null,
      allWidth: '',
      clientWdith: '',
      left1: 0,
      left2: 0,
      intervalId1: null,
      intervalId2: null,
      initFlag: false,
    };
  },
  props: {
    data: {
      type: Array,
    },
    className: {
      type: String,
      default: '',
    },
    duration: {
      type: Number,
      default: 50,
    },
    space: {
      type: Number,
      default: 0,
    },
    type: {
      type: String,
      default: 'transform',
    },
  },
  watch: {
    data(val) {
      this.list = val;
      if (this.list && this.list.length > 0) {
        this.$nextTick(() => {
          this.init();
        });
      }
    },
  },
  methods: {
    setStyle($el, left) {
      const el = $el;
      if (el && el.style) {
        if (this.type === 'position') {
          el.style.left = `${left}px`;
        } else {
          el.style.transform = `translate3d(${left}px,0,0)`;
        }
      }
    },
    startFn(num) {
      if (num === 1) {
        this.intervalId1 = setInterval(() => {
          this.left1 -= 1;
          this.setStyle(this.$refs.ListRef1, this.left1);
          this.check();
          if (!this.initFlag) {
            this.$refs.wrapper.style.visibility = 'initial';
            this.initFlag = true;
          }
        }, this.duration);
      } else if (num === 2) {
        this.intervalId2 = setInterval(() => {
          this.left2 -= 1;
          this.setStyle(this.$refs.ListRef2, this.left2);
          this.check();
        }, this.duration);
      }
    },
    stop(num) {
      if (num === 1) {
        clearInterval(this.intervalId1);
        this.intervalId1 = null;
        this.left1 = this.clientWidth;
        this.setStyle(this.$refs.ListRef1, this.left1);
      } else if (num === 2) {
        clearInterval(this.intervalId2);
        this.intervalId2 = null;
        this.left2 = this.clientWidth;
        this.setStyle(this.$refs.ListRef2, this.left2);
      }
    },
    init() {
      this.allWidth = this.$refs.ListRef1.offsetWidth;
      this.clientWidth = document.body.clientWidth;
      this.left1 = this.clientWidth;
      this.left2 = this.clientWidth;
      this.setStyle(this.$refs.ListRef2, this.left2);
      this.startFn(1);
    },
    check() {
      // 是否是正常的 总长度大于屏幕宽度
      const isNoraml = this.allWidth - this.clientWidth >= this.clientWidth;
      // 移动临界值
      const criticality = isNoraml ? (this.allWidth - this.clientWidth) + this.space : (this.allWidth + this.space);
      const left1 = Math.abs(this.left1);
      const left2 = Math.abs(this.left2);


      if (isNoraml) {
        if (left1 >= criticality && !this.intervalId2) {
          this.startFn(2);
        } else if (left1 > this.allWidth) {
          this.stop(1);
        }
      } else if (!isNoraml && -this.left1 >= criticality) {
        this.startFn(2);
        this.stop(1);
      }

      if (isNoraml) {
        if (left2 >= criticality && !this.intervalId1) {
          this.startFn(1);
        } else if (left2 > this.allWidth) {
          this.stop(2);
        }
      } else if (!isNoraml && -this.left2 >= criticality) {
        this.startFn(1);
        this.stop(2);
      }
    },
  },
  mounted() {
    if (this.data && this.data.length > 0) {
      this.list = this.data;
      this.$nextTick(() => {
        this.init();
      });
    }
  },
};
</script>
<style type="text/css">
  html,body{
    height: 100%;
    width: 100%;
  }
  *{
    margin: 0;
    padding: 0;
  }
</style>
<style lang="less" scoped>
.marquee-wrapper {
  width: 100%;
  height: 56px;
  line-height: 56px;
  background: #33BB33;
  visibility: hidden;
  position:relative;
  overflow: hidden;
  .marquee-list{
    position: absolute;
    width: max-content;
    color: #fff;
    font-size: 28px;
    overflow: hidden;
    & > span {
      margin-right: 18px;
      display: inline-block;
    }
  }
}
</style>
