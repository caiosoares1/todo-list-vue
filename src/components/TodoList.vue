<template>
 
 <div class="todo-list">
    <h1>
        TODO LIST
    </h1>
    <div class="input-group">

        <input v-model="newTask" @keyup.enter="addTask" type="text" placeholder="Adicionar novo item na lista..."/>
        <button @click="addTask">Adicionar</button>
    </div>

    <ul>
        <li v-for="(task, index) in tasks" :key="index">

          <div v-if="task.isEditing" class="edit-group">
            <input v-model="task.text" @keyup.enter="finishEdit(task)" class="edit-input"/>
            <button @click="finishEdit(task)" class="save-button">Salvar</button>

          </div>
          
          <div v-else class="task-group">
            {{ task.text }}

            <div class="manage-task">
              <button @click="editTask(index)"><font-awesome-icon icon="edit"/></button>
              <button @click="removeTask(index)"><font-awesome-icon icon="trash" /></button>

            </div>
          </div>
            
        </li>
    </ul>
 </div>

</template>

<script>
    export default {
      
        data() {
            return {
                newTask: '',
                tasks: []
            }
        
    },

    

    methods: {
        addTask() {
            if (this.newTask.trim() && !this.tasks.some(task => task.text === this.newTask.trim())) {
                this.tasks.push({text: this.newTask, isEditing: false});
                this.newTask = '';

            }
        },
        removeTask(index) {
            this.tasks.splice(index, 1);
        },
        editTask(index, newText) {
            this.tasks[index].isEditing = true;
            if (newText && newText.trim() !== '') {
                this.tasks[index].text = newText.trim();
                this.tasks[index].isEditing = false;
            }
        },
        finishEdit(task) {
        task.isEditing = false;
        }
      }
    }
</script>

<style scoped>
.todo-list {
    
  max-width: 400px;
  margin: auto;
}

h1 {
  color: aliceblue;
  text-align: center;
  margin: 2rem;
}

.input-group {
    display: flex;
    justify-content: space-between;
    gap: 1rem;
    margin: 2rem 0;

}
input {
  width: 100%;
  padding: 10px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  color: white;
  border: 1px solid #ccc;
  margin-bottom: 5px;
}
button {
  background-color: #F28D6B;
  color: white;
  text-decoration: double;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
.manage-task {
  display: flex;
  gap: 5px;
}
.task-group {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.edit-group {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-height: 2rem;
}

.edit-input {
  width: 80%;
}

.save-button {
  width: auto;
}
</style>
