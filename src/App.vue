<template>
    <div id="app" class="container">
        <h2>Tareas</h2>

        <ul class="list-group tasks">
            <li is="app-task" v-for="(task, index) in tasks"
                :tasks="tasks" :task="task" :index="index" @remove="deleteTask"></li>
        </ul>

        <p><a @click="deleteCompleted">Eliminar tareas completadas</a></p>

        <form @submit.prevent="createTask" class="new-task-form">
            <input v-model="new_task" type="text" class="form-control">
            <button class="btn btn-primary">Crear tarea</button>
        </form>

        <footer class="footer">
            <p>Manuel Uso / Curso Vue</p>
        </footer>
    </div>
</template>

<script>
import Task from './Task.vue'
export default {
    components: {
        'app-task': Task
    },
    methods: {
        createTask: function () {
            this.tasks.push({
                description: this.new_task,
                pending: true,
                editing: false
            });
            this.new_task = '';
        },
        deleteTask: function (index) {
            this.tasks.splice(index, 1);
        },
        deleteCompleted: function () {
            this.tasks = this.tasks.filter(function (task) {
                return task.pending;
            });
        }
    },
    data: function () {
        return {
            new_task: '',
            tasks: [
                {
                    description: 'Aprender Vue.js',
                    pending: true,
                },
                {
                    description: 'Configurar Entorno de Trabajo',
                    pending: true,
                },
                {
                    description: 'Subirlo al Repositorio',
                    pending: false,
                }
            ]
        }
    }
}
</script>