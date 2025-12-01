<template>
  <div :class="['app-container', pageClass]">
    <ProductCard :product="savedProduct">
      <Controls 
        @prev="prevProduct"
        @next="nextProduct"
        @random="randomProduct"
      />
    </ProductCard>
  </div>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'
import Controls from '@/components/Controls.vue'

export default {
  name:"Home",
  components:{ ProductCard, Controls },
  data(){
    return{
      index:1,
      savedProduct:null
    }
  },
  computed:{
    pageClass(){
      const cat = this.savedProduct?.category?.toLowerCase() || ''
      if(cat.includes("men")) return 'page-men'
      if(cat.includes("women")) return 'page-women'
      return 'page-unavailable'
    }
  },
  methods:{
    async fetchByIndex(i){
      try{
        const res = await fetch(`https://fakestoreapi.com/products/${i}`)
        const data = await res.json()
        const cat = data.category?.toLowerCase()

        if(cat === "men's clothing" || cat === "women's clothing"){
          this.savedProduct = data
        } else {
          this.savedProduct = null
        }
      }catch(e){
        this.savedProduct = null
      }
    },
    nextProduct(){
      this.index++
      if(this.index > 20) this.index = 1
      this.fetchByIndex(this.index)
    },
    prevProduct(){
      this.index--
      if(this.index < 1) this.index = 20
      this.fetchByIndex(this.index)
    },
    randomProduct(){
      this.index = Math.floor(Math.random()*20)+1
      this.fetchByIndex(this.index)
    }
  },
  mounted(){
    this.fetchByIndex(1)
  }
}
</script>
