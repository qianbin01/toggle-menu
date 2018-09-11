<template>
  <div class="toggle_menu_container">
    <toggle-menu position="LT"
                 menuBg="white"
                 itemBg="white"
                 :menuItems="menuItems"
                 @clickMenu="clickMenu"
                 baseDistance="150"></toggle-menu>
  </div>
</template>

<script>
  import toggleMenu from './toggleMenu'

  export default {
    name: 'index',
    data() {
      return {
        menuItems: [
          {name: 'menu1', src: require('../assets/emoji.png')},
          {name: 'menu2', src: require('../assets/cart.png')},
          {name: 'menu3', src: require('../assets/folder.png')},
          {name: 'menu4', src: require('../assets/home.png')},
          {name: 'menu5', src: require('../assets/my.png')},
        ]
      }
    },
    methods: {
      clickMenu(item, index) {
        console.log(item, index)
      }
    },
    components: {
      toggleMenu
    },

  }
</script>

<style scoped>


</style>
