<script setup>

    import 'bootstrap/dist/css/bootstrap.min.css';
    import 'bootstrap/dist/js/bootstrap.bundle.min.js';
    import { ref, onMounted } from 'vue';
    import axios from 'axios';

    const characters = ref([]);
    const total_characters = ref(0);
    const search_name = ref('');
    const search_status = ref('');
    const page = ref(1);
    const loading = ref(false);
    const error = ref(null);

    // Função para buscar personagens da API
    const fetchCharacters = async () => {
    
        loading.value = true;
        error.value = null;
        
        try {
            const response = await axios.get(`https://rickandmortyapi.com/api/character`, {
                params: {
                    name: search_name.value,
                    status: search_status.value,
                    page: page.value
                }
            });
            characters.value = response.data.results.map(personagem => ({
                image: personagem.image,
                name: personagem.name,
                status: personagem.status,
                episode: personagem.episode.length,
                location: personagem.location.name
            }));
            total_characters.value = response.data.info.count;
        } catch (err) {
            error.value = 'Erro ao buscar personagens';
            console.error(err);
        } finally {
            loading.value = false;
        }
    };

    // Buscar personagens ao carregar a página
    onMounted(fetchCharacters);

    // Função para mudar de página
    const changePage = (direction) => {
        page.value += direction;
        fetchCharacters();
    };
</script>

<template>
  <div class="container py-4">
    <div class="card shadow-lg p-4">
      <!-- Filtros -->
      <div class="row g-2 align-items-center mb-4">
        <div class="col-md-4">
          <input
            v-model="search_name"
            type="text"
            class="form-control"
            placeholder="Search by name"
          />
        </div>
        <div class="col-md-3">
          <select v-model="search_status" class="form-select">
            <option value="">All status</option>
            <option value="Alive">Alive</option>
            <option value="Dead">Dead</option>
            <option value="unknown">Unknown</option>
          </select>
        </div>
        <div class="col-md-3">
          <button @click="fetchCharacters" class="btn btn-primary w-100">
            Search
          </button>
        </div>
      </div>

      <!-- Mensagens de erro ou carregamento -->
      <div v-if="loading" class="text-center text-secondary">Loading...</div>
      <div v-if="error" class="alert alert-danger text-center">
        {{ error }}
      </div>

      <!-- Tabela -->
      <div v-if="characters.length" class="table-responsive">
        <table class="table table-striped table-bordered">
          <thead class="table-dark">
            <tr>
              <th>Image</th>
              <th>Name</th>
              <th>Status</th>
              <th>Total Episodes</th>
              <th>Location</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="character in characters" :key="character.name">
              <td>
                <img
                  :src="character.image"
                  :alt="character.name"
                  class="rounded-circle"
                  width="50"
                  height="50"
                />
              </td>
              <td class="fw-bold">{{ character.name }}</td>
              <td>
                <span
                  class="badge"
                  :class="{
                    'bg-success': character.status === 'Alive',
                    'bg-danger': character.status === 'Dead',
                    'bg-secondary': character.status === 'unknown',
                  }"
                >
                  {{ character.status }}
                </span>
              </td>
              <td class="text-center">{{ character.episode }}</td>
              <td>{{ character.location }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Paginação -->
      <nav v-if="characters.length">
        <ul class="pagination justify-content-center mt-3">
          <li class="page-item" :class="{ disabled: page === 1 }">
            <a class="page-link" href="#" @click.prevent="changePage(-1)">
              Previous
            </a>
          </li>
          <li class="page-item">
            <a class="page-link" href="#" @click.prevent="changePage(1)">
              Next
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>