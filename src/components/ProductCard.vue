<template>
  <div :class="classItem" @click="onEmit(card.id)">
    <img :src="card.image" :alt="card.image" />
    <div class="best__item-title">{{ card.name }}</div>
    <div class="best__item-price">{{ card.price | addCurrency }}</div>
  </div>
</template>

<script>
export default {
  props: {
    classItem: {
      type: String,
    },
    card: {
      type: Object,
      required: true,
    },
  },
  methods: {
    onEmit(id) {
      this.$emit("onNavigate", id);
    },
  },
};
</script>
