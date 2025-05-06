    <script setup>
    const props = defineProps({
    tarefas: Array
    });
    </script>

    <template>
    <ul class="list-group mt-4">
        <li 
        class="list-group-item" 
        v-for="(tarefa, index) in tarefas" 
        :key="index"
        >
        <input 
            @change="evento => tarefa.finalizada = evento.target.checked" 
            :checked="tarefa.finalizada" 
            :id="tarefa.título" 
            type="checkbox"
        />
        <label 
            :class="{ done: tarefa.finalizada }" 
            class="ms-3" 
            :for="tarefa.título"
        >
            {{ tarefa.título }}
        </label>
        </li>
    </ul>
    </template>

    <style scoped>
    .done {
    text-decoration: line-through;
    }
    </style>
