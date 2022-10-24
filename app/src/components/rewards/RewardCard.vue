<template>
  <div 
    class="grid grid-cols-2 p-4 mb-4 border-2 border-blue-800 rounded-lg"
  >
    <h3 class="text-xl">{{ reward.name }}</h3>
    <p class="text-5xl">{{ reward.point }}</p>

    <div class="italic">
      <slot></slot>
    </div>

    <div class="text-2xl font-bold">
      <slot name="total_amount"></slot>
    </div>
  

    
      <button @click="onClickButton()"
        class="px-2 py-1 border rounded-xl">
        Redeem
      </button>
      
    <div class="grid grid-cols-2">
      <button @click="onClickLike()"
        class="px-2 py-1 mx-4 bg-yellow-200 border rounded-xl">
        {{ likeCount }} Likes
      </button>

      <button @click="onClickCounter()"
        class="px-2 py-1 mx-4 bg-green-200 border rounded-xl">
        {{ counter_store.counter }} |
        {{ counter_store.doubleCount }}
      </button>
    </div>

    
  </div>
</template>

<script>
import { useCounterStore } from '@/stores/counter.js'

export default {
  setup() {
    const counter_store = useCounterStore()
    return { counter_store }
  },
  data() {
    return {
      likeCount: 0
    }
  },
  props: {
    reward: Object,
    url: {
      type: String,
      default: ''
    }
  },
  methods: {
    onClickLike() {
      this.likeCount++
    },
    onClickCounter() {
      this.counter_store.increment()
    },
    onClickButton() {
      if (this.url != '') {
        this.$router.push(this.url)
      }
    }
  }
}
</script>

<style scoped>
.my-style {
  @apply block p-2 bg-pink-300 w-20;
}
</style>