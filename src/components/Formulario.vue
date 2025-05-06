    <script setup>
    const props = defineProps({
    cadastraTarefa: Function,
    tarefaTemp: String,
    trocarFiltro: Function,
    editaTarefaTemp: Function
    });
    </script>

    <template>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
        <div class="col">
            <input 
            :value="tarefaTemp" 
            @input="editaTarefaTemp" 
            required 
            type="text" 
            placeholder="Digite aqui a descrição da tarefa" 
            class="form-control"
            >
        </div>
        <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="trocarFiltro" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
        </div>
    </form>
    </template>
