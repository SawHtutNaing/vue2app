<template>
  

    <div class="container">
    <div class="row justify-content-center">
        <div class="col-12 col-md-4">
            <div class="my-5">
                <Title title="Vue To Do App"></Title>

                <div class="form-row mb-3">
                    <div class="col-10">
                        <input type="text" class="form-control form-control-lg" v-model="newMessage" @keyup.enter="create()" placeholder="Say Something">
                    </div>
                    <div class="col-2">
                        <button class="btn btn-primary btn-lg w-100" @click="create()">
                            <i class="fas fa-plus-circle"></i>
                        </button>
                    </div>
                </div>

                <div class="d-flex justify-content-between">
                    <p class="mb-0 font-weight-bold">Job List{{ lists.length > 1 ? "s" : "" }}</p>
                    <p v-if="lists.length>0 && doneTotal===lists.length" class="badge badge-success badge-pill">
                        All Done <i class="fas fa-check-circle"></i>
                    </p>
                    <p v-else class="badge badge-primary badge-pill">
                        Done {{ doneTotal }}
                    </p>
                </div>

                <ul class="list-group">
                    <li v-if="lists.length === 0" class="list-group-item text-center">
                        There is no job 🥺
                    </li>
                  <List v-for="list in lists"  :list = " list"  :key="list.id"  @del="del"></List>
                </ul>
            </div>
        </div>
    </div>




  </div>
</template>

<script>
import List from './components/List.vue'
import Title from './components/Title.vue'
  export default {
  components: { Title, List },
    
  data() {
    return {
        currentId : 0,
        newMessage : "",
        lists : [

        ]
    }
  },
    computed :{
        doneTotal(){
            return this.lists.filter(el=>el.isDone === true).length
        }
    },
    methods : {
        create(){
            this.currentId++
            this.lists.push({
                id: this.currentId,
                message : this.newMessage,
                isDone : false,
             
            });
            this.newMessage = "";
        },
        del(x){
            // if(confirm('Are U Sure to delete ?')){
            setTimeout(()=>this.lists = this.lists.filter(el => el.id !== x),500)
            // }
        }
    }


  }
</script>

<style>

    .done{
            text-decoration: line-through !important;
            animation: 0.5s shakeX;
        }
        .created{
            animation: 0.5s fadeInDown;
        }
        .deleted{
            animation: 0.5s zoomOut;
        }

</style>