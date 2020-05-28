<template>
  <div id="app">
    <nav>
      <div>
        <b-navbar type="dark" variant="dark">
          <b-navbar-nav>
            <b-nav-item @click="selectedTab('view')">View</b-nav-item>
            <b-nav-item @click="selectedTab('upload')">Upload</b-nav-item>
          </b-navbar-nav>
        </b-navbar>
      </div>
    </nav>
   
   
    <ViewComponent  v-if="tab==='view'"/>
    <UploadComponent  v-if="tab==='upload'"/>
  </div>
</template>

<script>

import ViewComponent from './components/view.vue'
import UploadComponent from './components/upload.vue'

export default {
  name: 'App',
  components: {
   UploadComponent,
    ViewComponent
  }, data() {
    return {
      tab: 'view'
    }
  },
  methods: {
    selectedTab(option){
      this.tab = option
      console.log(this.tab)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
</style>
