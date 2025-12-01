<template>
  <div class="product-card">
    <img v-if="product" :src="product.image" class="product-image" />
    <div class="product-body">
      <h3 class="product-title">{{ product?.title || 'Unavailable Product' }}</h3>
      <p class="product-category">{{ product?.category || '-' }}</p>
      <p v-if="product?.price" class="product-price">Rp {{ formatPrice(product.price) }}</p>
      <p v-else>Product tidak tersedia untuk kategori ini.</p>

      <div class="controls">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:"ProductCard",
  props:{ product:Object },
  methods:{
    formatPrice(price){
      return (price * 15000).toLocaleString()
    }
  }
}
</script>
