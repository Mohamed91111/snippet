<template>
    <div>
       <form>
            <div class="form-group">
                <label for="exampleFormControlInput1">Title</label>
                <input v-model="title" type="text" class="form-control" id="exampleFormControlInput1" placeholder="Title...">
            </div>
            <div class="text-area">
                <label for="exampleFormControlTextarea1">Content</label>
                <textarea v-model="content" class="form-control" id="exampleFormControlTextarea1" rows="8"></textarea>
            </div>
            <div class="upload-button">
                <button @click="newSnippet()" type="button" class="btn btn-success btn-block">Upload</button>
                
            </div>
        </form>
    </div>
</template>


<script>
import axios from 'axios'

export default {
  name: 'UploadComponent',
  data() {
    return {
        title: '',
        content: ''
    }
  },
  methods: {
      newSnippet(){
           axios.post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?', { add:'', title: this.title, content: this.content})
                    .then(res => console.log(res.data.message))
                    .catch(error => console.log(error))
                    this.title = ''
                    this.content = ''
      }
   
  }
}
</script>

<style scoped>
.form-group{
    margin: 50px 50px;
}
.text-area{
     margin: 50px 50px;
}

.upload-button{
    display: flex;
    margin: 50px;
}
</style>