<template>
  <div v-if="loading">
    <slot name="progress"></slot>
  </div>
</template>

<script>
export default {
  name: "InfiniteScrollProvider",
  props: {
    haseItem : Boolean,
    loading: Boolean
  },
  data(){
    return{
      timerInterval: null,
      timeLimit: 2,
      timePassed: 0,
      waiting: false
    }
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll.bind(this));
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll.bind(this));
  },
  methods: {
    handleScroll() {
      const bottomOfWindow =window.innerHeight + window.pageYOffset > document.body.offsetHeight;
      if (bottomOfWindow && this.haseItem) {
        if (!this.waiting){
          this.$emit("load-more");
          this.timePassed = 0
          this.timer()
        }
      }
    },
    timer(){
      this.waiting = true
      this.timerInterval = setInterval(() => {
        this.timePassed += 1
        if (this.timePassed >= this.timeLimit) {
          this.waiting = false
          clearInterval(this.timerInterval)
        }
      }, 1000)
    }
  }
}
</script>

<style scoped>

</style>
