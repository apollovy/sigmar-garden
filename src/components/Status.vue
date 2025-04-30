<template>
  <div 
    class="status-container" 
    :style="`background-image: url('./atoms/${status.element}.png')`" 
    :class="{ 
      fade: status.count === 0,
      highlighted: isSelected
    }"
    @click="onClick"
  >
    <span class="num-left" :class="{ warning: status.oddWarn && status.count % 2 === 1 }">{{ status.showCount ? status.count : '' }}</span>
  </div>
</template>

<script>
export default {
  props: {
    status: Object,
    selectedStatus: String
  },
  computed: {
    isSelected() {
      return this.selectedStatus === this.status.element
    }
  },
  methods: {
    onClick() {
      this.$emit('status-click', this.status.element)
    }
  }
}
</script>

<style scoped>
.status-container {
  background-repeat: no-repeat;
  background-position: center;
  background-size: 100% 100%;
  height: 65%;
  width: 6.5%;
  position: relative;
  cursor: pointer;
  transition: filter 0.3s ease;
}
.status-container span {
  font-size: 80%;
  color: #eee;
  position: absolute;
  right: -10%;
  top: -10%;
}
.status-container span.warning {
  color: red;
}
.status-container.fade {
  filter: brightness(0.5);
}
.status-container.highlighted {
  animation: pulse 0.8s infinite;
}

@keyframes pulse {
  0% {
    filter: brightness(0.8) drop-shadow(0 0 5px rgba(255, 255, 255, 0.7));
  }
  50% {
    filter: brightness(1.2) drop-shadow(0 0 15px rgba(255, 255, 255, 1));
  }
  100% {
    filter: brightness(0.8) drop-shadow(0 0 5px rgba(255, 255, 255, 0.7));
  }
}
</style>
