<template>
  <div class="global-warpper">
    <Header
    @sorting="sort"
    ></Header>
    <div class="container">
      <Form
      @added="addItem"
      ></Form>
        <div class="item-wrapper">
          <transition-group class="item-wrapper" name="list" tag="p">
              <Item
              v-bind:key="item"
              class="list-item"
              v-bind:item="item"
              v-for="item in items"
              @removeItem="removeItem"
              ></Item>
          </transition-group>
        </div>
      </div>
    </div>

</template>

<script>

import Form from '@/components/form'
import Item from '@/components/item'
import Header from '@/components/header'

export default {
  name: 'App',
  data() {
    return {
      items: [
        {
        itemName: "Item 1",
        itemInfo: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        itemImgURL: "https://shop.instantphotoclub.ru/wp-content/uploads/sites/2/2020/01/best-istant-cameras-polaroid-onestep2.jpg",
        itemPrice: 100
        },
        {
        itemName: "Item 2",
        itemInfo: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        itemImgURL: "https://shop.instantphotoclub.ru/wp-content/uploads/sites/2/2020/01/best-istant-cameras-polaroid-onestep2.jpg",
        itemPrice: 10700
        },
        {
        itemName: "Item 3",
        itemInfo: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        itemImgURL: "https://shop.instantphotoclub.ru/wp-content/uploads/sites/2/2020/01/best-istant-cameras-polaroid-onestep2.jpg",
        itemPrice: 1000
        },{
        itemName: "Item 4",
        itemInfo: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        itemImgURL: "https://shop.instantphotoclub.ru/wp-content/uploads/sites/2/2020/01/best-istant-cameras-polaroid-onestep2.jpg",
        itemPrice: 15000
        },
        {
        itemName: "Item 5",
        itemInfo: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        itemImgURL: "https://shop.instantphotoclub.ru/wp-content/uploads/sites/2/2020/01/best-istant-cameras-polaroid-onestep2.jpg",
        itemPrice: 100000
        },
      ]
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    removeItem(item) {
      this.items.splice(this.items.indexOf(item), 1);
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    sort(type) {
      if (type == "По возрастанию цены") {
        this.items.sort((a, b) => a.itemPrice > b.itemPrice ? 1 : -1);
      }
      if (type == "По убыванию цены") {
        this.items.sort((a, b) => a.itemPrice < a.itemPrice ? 1 : -1);
      }
      if (type == "По наименованию") {
        this.items.sort((a, b) => a.itemName > b.itemName ? 1 : -1);
      }
    },
  },
  beforeMount() {
    if (localStorage.getItem('items') != null) {
      this.items = JSON.parse(localStorage.getItem('items'));
    }
  },
  mounted() {
    //-preloader
  },
  components: {
    Form,
    Item,
    Header,
}
}
</script>

<style lang="scss" scoped>



.list-leave-active {
  transition: all 0.3s;
  position: absolute;
}
.list-enter, .list-leave-to  {
  opacity: 0;
}
.list-move {
  transition: transform 0.3s;
}


/* source-sans-pro-regular - latin_cyrillic */
@font-face {
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  src: url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.woff2') format('woff2'), /* Super Modern Browsers */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.woff') format('woff'), /* Modern Browsers */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.ttf') format('truetype'), /* Safari, Android, iOS */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-regular.svg#SourceSansPro') format('svg'); /* Legacy iOS */
}
/* source-sans-pro-600 - latin_cyrillic */
@font-face {
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  src: url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.woff2') format('woff2'), /* Super Modern Browsers */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.woff') format('woff'), /* Modern Browsers */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.ttf') format('truetype'), /* Safari, Android, iOS */
       url('@/assets/fonts/source-sans-pro-v21-latin_cyrillic-600.svg#SourceSansPro') format('svg'); /* Legacy iOS */
}
/*Inter*/
@font-face {
  font-family: Inter;
  src: url('@/assets/fonts/Inter-VariableFont_slnt\,wght.ttf');
}

body {
  background-color: aquamarine;
}

#app {
  .global-warpper {
    margin: 0px;
    padding-right: 32px;
    padding-left: 32px;
  }
 
  .container {
    display: flex;
  }

  @media (max-width: 740px) {
    .container {
      flex-direction: column;
    }
  }

  .item-wrapper {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
}
</style>
