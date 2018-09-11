引入组件
```vue
import toggleMenu from './toggleMenu'
```

在 components声明
```vue
components: {
     toggleMenu
},
```

template中使用
```vue
menuItems: [
       {name: 'menu1', src: require('../assets/emoji.png')},
       {name: 'menu2', src: require('../assets/cart.png')},
       {name: 'menu3', src: require('../assets/folder.png')},
       {name: 'menu4', src: require('../assets/home.png')},
       {name: 'menu5', src: require('../assets/my.png')},
]
<toggle-menu :menuItems="menuItems"
             @clickMenu="clickMenu"
             ></toggle-menu>
```
属性一栏

| 属性名 | 用处 | 默认值 | 是否必须 |
| ------ | ------ | ------ | ------|
| position | 四个方位(LT、LB、RT、RB) | LT | 否
| menuBg | 菜单背景 | white | 否
| menuSrc | 菜单图片 | 一个菜单图片 | 否
| itemBg | 按钮背景 | white | 否
| width | 按钮宽度 | 50px | 否
| baseDistance | 位移距离，若item很多，可适当提高 | 150px | 否
| menuItems | 菜单数组 | 无 | 是


方法

clickMenu   参数（item,index）  点击的对象及其下标
