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
            {{ task }}
            <button @click="removeTask(index)">Remover</button>
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
            if (this.newTask.trim() !== '' && !this.tasks.includes(this.newTask)) {
                this.tasks.push(this.newTask);
                this.newTask = '';

            }
        },
        removeTask(index) {
            this.tasks.splice(index, 1);
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
</style>
