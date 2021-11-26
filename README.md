# vue-infinite-scroll-provider

## 🎯 install
```
$ yarn add vue-infinite-scroll-provider
# npm install vue-infinite-scroll-provider --save
```


## 🚀 Usage
```vue
<template>
  <div id="app">
    <infinite-scroll-provider @load-more="fetchData" :hase-item="haseItem" :loading="loading">
      <template v-slot:progress>
        <div style="background: blue;color: white; position: fixed;height: 50px;bottom: 0;left: 0;right: 0;">loading
          data please wait ...
        </div>
      </template>
    </infinite-scroll-provider>
</template>

<script>
import InfiniteScrollProvider from "vue-infinite-scroll-provider";

export default {
  name: 'App',
  data() {
    return {
      rows: 50,
      haseItem: true,
      loading: false,
      page: 0
    }
  },
  components: {
    InfiniteScrollProvider
  }, methods: {
    fetchData() {
      console.log('get data from server')
      this.page++

      if (this.haseItem) {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.rows += 50
          if (this.page === 5) {
            this.haseItem = false
          }
        }, 3000)
      }

    }
  }
}
</script>

<style>

</style>


```

