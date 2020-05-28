<template>
    <div>
                <div>
                    <h2>{{filter}}</h2>
            <b-dropdown id="dropdown-1" text="Filter by..." class="m-md-2">
                <b-dropdown-item @click="filterUsed('latest')">Latest</b-dropdown-item>
                <b-dropdown-item @click="filterUsed('best')">Best</b-dropdown-item>
            </b-dropdown>
            </div>
            
            <div  class = "snippet-container" >
                <b-card bg-variant="dark" text-variant="white" v-for="snippet in snippets" v-bind:key="snippet.id" class="card" >
                    <h2>{{snippet.title}}</h2>
                    <b-card-text>
                        <div class="content">
                           <p>{{snippet.content}}</p>
                        </div>
                        
                    </b-card-text>
                    <b-button class="delete-button" block  variant="danger" @click="remove(snippet.id)">Delete</b-button>
                </b-card>
            </div>
    </div>
</template>


<script>
 import axios from 'axios'

export default {
 
  name: 'ViewComponent',
  data() {
    return {
      filter: 'latest',
      snippets: []
    }
  },
  methods: {
   filterUsed(choice){
       this.filter = choice
       if(choice === 'latest'){
            this.getLatest()
       }else{
            this.getBest()
       }
      
   },
   getLatest(){
        
            axios.get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest')
            .then(res => this.snippets = res.data)
            .catch(error => console.log(error))
   },
    getBest(){
           
            axios.get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?best')
            .then(res => this.snippets = res.data)
            .catch(error => console.log(error))
           
    },
    remove(id){
            
           
            axios.post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?', {delete:'',id:id})
            .then(res => {console.log(res.data.message)
            this.getLatest()
            })
            .catch(error => console.log(error))
            
        }
    
  }, created(){
            this.getLatest()
           
    }   
}
</script>

<style scoped>
.snippet-container{
        border: solid 2px;
    width: 700px;
    display: inline-block;
    min-height: 70vh;
    max-height: 70vh;
    padding: 10px;
    overflow: scroll;
    overflow-x: hidden;
}

.card{
    margin-top: 10px !important;
    margin-bottom: 10px !important;
}


</style>