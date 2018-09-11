<template>
  <div>
    <div class="menu_container" ref="menuHome" @click="toggleMenu">
      <img :src="menuSrc">
    </div>
    <div class="menu_item" v-for="(item,index) in menuItems" :id="item.name" @click="clickMenu(item,index)">
      <img :src="item.src">
    </div>
  </div>
</template>

<script>
  export default {
    name: "toggleMenu",
    props: {
      menuSrc: {
        default: require('../assets/menu.png')
      },
      position: {
        default: 'LT'
      },
      width: {
        default: 50,
      },
      baseDistance: {
        default: 150,
      },
      menuBg: {
        default: 'white'
      },
      itemBg: {
        default: 'white'
      },
      menuItems: {
        type: Array,
      }
    },
    data() {
      return {
        openFlag: false,
        operators: ['+', '+'],

      }
    },
    mounted() {
      this.$refs.menuHome.style.width = this.width + 'px';
      this.$refs.menuHome.style.height = this.width + 'px';
      this.$refs.menuHome.style.lineHeight = this.width + 'px';
      this.$refs.menuHome.style.background = this.menuBg;
      this.menuItems.forEach((item) => {
        let el = document.getElementById(item.name);
        el.style.width = `${this.width * 0.8}px`;
        el.style.height = `${this.width * 0.8}px`;
        el.style.lineHeight = `${this.width * 0.8}px`;
        el.style.background = this.itemBg;
      });
      switch (this.position) {
        case 'LT':
          this.$refs.menuHome.style.left = '20px';
          this.$refs.menuHome.style.top = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.left = '26px';
            el.style.top = '26px';

          });
          this.operators = ['+', '+'];
          break;
        case 'RT':
          this.$refs.menuHome.style.right = '20px';
          this.$refs.menuHome.style.top = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.right = '26px';
            el.style.top = '26px';
          });
          this.operators = ['-', '+'];
          break;
        case 'LB':
          this.$refs.menuHome.style.left = '20px';
          this.$refs.menuHome.style.bottom = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.left = '26px';
            el.style.bottom = '26px';
          });
          this.operators = ['+', '-'];
          break;
        case 'RB':
          this.$refs.menuHome.style.right = '20px';
          this.$refs.menuHome.style.bottom = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.right = '26px';
            el.style.bottom = '26px';
          });
          this.operators = ['-', '-'];
          break;
        default:
          this.$refs.menuHome.style.left = '20px';
          this.$refs.menuHome.style.top = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.left = '26px';
            el.style.top = '26px';
          });
          this.operators = ['+', '+'];
          break;
      }
    },
    methods: {
      toggleMenu() {
        if (!this.openFlag) {
          this.menuItems.forEach((item, index) => {
            this.toggleMenuTransition(item.name, index, false)
          });
          this.$refs.menuHome.style.transform = 'rotate(360deg)';
        } else {
          this.menuItems.forEach((item, index) => {
            this.toggleMenuTransition(item.name, index, true)
          });
          this.$refs.menuHome.style.transform = 'rotate(0)';
        }
        this.openFlag = !this.openFlag;
      },
      toggleMenuTransition(name, index, revert) {
        let oneArea = 90 / (this.menuItems.length - 1);
        let axisX = Math.sin((this.menuItems.length - 1 - index) * oneArea * 2 * Math.PI / 360);
        let axisY = Math.cos((this.menuItems.length - 1 - index) * oneArea * 2 * Math.PI / 360);
        let el = document.getElementById(name);
        let that = this;
        if (!revert) {
          setTimeout(function () {
            el.style.transitionDuration = '200ms';
            el.style.transform = `translate(${that.operators[0]}${that.baseDistance * axisX}px,${that.operators[1]}${that.baseDistance * axisY }px)`;
          }, index * 100)
        } else {
          el.style.transitionDuration = '200ms';
          el.style.transform = `translate(0,0)`;
        }
      },
      clickMenu(item, index) {
        this.$emit('clickMenu', item, index)
      }
    }
  }
</script>

<style scoped>
  .menu_container {
    position: absolute;
    z-index: 100;
    border-radius: 50%;
    transition-duration: 400ms;
    text-align: center;
    border: #efefef 3px solid;
    box-shadow: aliceblue 1px 1px 1px;
  }

  .menu_item {
    position: absolute;
    border-radius: 50%;
    z-index: 99;
    border: #efefef 3px solid;
    text-align: center;
    box-shadow: aliceblue 1px 1px 1px;
  }

  img {
    width: 50%;
    transform: translate(-5%, 20%);
  }
</style>
