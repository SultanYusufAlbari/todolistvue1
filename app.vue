<template>
  <div>
    <h1>Todo List</h1>
    <div v-show="tasks.length === 0">
      <p>No tasks available.</p>
    </div>
  </div>
  <div class="list-task">
      <div v-for="(item,index) in tasks" :key="index" class="item-task d-flex align-items-start border-bottom pt-3 pb-4">
      <input
      type="checkbox"
      class="me-2 mt-2"
      id="task"
      name="status"
      :checked="item.isDone"
      @change="updateTask(index)"
      >
      <div class="d-flex flex-column">
          <div class="title-task mb-1" :class="{ 'completed': item.isDone }">
          {{ item.title }}
          </div>
          <div class="description-task small text-muted">
          {{ item.description }}
          </div>
          <button @click="deleteTask(item)">Delete</button>
      </div>
      </div>
  </div>

  <div class="action py-2">
      <a href="#" class="add-button" v-if="!isCreating" @click="isCreating =!isCreating">Add Task</a>
      <div class="add-card" v-else>
          <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                  <input v-model="titleValue" class="form-control" border-0 mb-2 placeholder="Title" type="text">
                  <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
              </div>
      </div>
      <div class="button-wrapper d-flex">
        <button type="button" class="btn btn-primary btn-sm" @click="addTask">Save</button>
        <button type="button" class="btn btn-outline-secondary" @click="isCreating =!isCreating">Cancel</button>
      </div>
  </div>
</div>
</template>

<script>
// import 'bootstrap/dist/css/bootstrap.css'
// import 'bootstrap-vue/dist/bootstrap-vue.css'
export default {
  data() {
      return{
          //daftar task
      tasks: [
          {
              id: 1,
              title: 'Task 1',
              description: 'ini deskripsi',
              isDone: false,
              show: false,
              items: ['Item 1', 'Item 2', 'Item 3'],
              //Status saat menambahkan task
          }
      ],
      isCreating: false,
      titleValue: '',
      descriptionValue: '',
    }
  },
  methods: {
      addTask() {
        console.log('title :', this.titleValue);
        console.log('description :', this.descriptionValue);
        this.tasks.push({
          id: this.tasks.length + 1,
          title: this.titleValue,
          description: this.descriptionValue,
          isDone: false,
        })
        //untuk mengosongkan data ketika sudah disave
        this.titleValue = '';
        this.descriptionValue = '';
        console.log(this.tasks);
      },
      deleteTask(){
        this.tasks.splice(this.tasks.length - 1, 1);
      },
      updateTask(index){
        this.tasks[index].isDone = !this.tasks[index].isDone;
      }
    } 
}
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>