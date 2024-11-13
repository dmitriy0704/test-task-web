<script>
import axios from 'axios'
import { ref } from 'vue'

export default {
  name: 'CreateEmployee',
  components: {},
  data() {
    return {
      selected: ref(''),
      prof_list: {},
      empl: {
        fio: '',
        description: '',
        professions: ''
      },
      isSaving: false,
    };
  },
  methods: {
    async getProfessionList() {
      const {data} = await axios.get(
          "http://localhost:8080/api/prof?list",
      );
      this.prof_list = data;
    },
    handleSave() {
      this.isSaving = true
      axios.post('http://localhost:8080/api/empl', this.empl)
          .then(response => {
            this.isSaving = false
            this.empl.fio = ""
            this.empl.profession = ""
            this.empl.description = ""
            return response
          })
          .catch(error => {
          });
    },
  },

  beforeMount() {
    this.getProfessionList();

  },

};

</script>

<template>
  <div class="col-md-12">
    <h3 class="green">Создать сотрудника</h3>
  </div>
  <div class="card">

    <div>
      <ul class="list-group">
        <li style="list-style: none" v-for="(item, index) in prof_list"
            :key="index"
            class="list-group-item">
          {{ index + 1 }}. <i>Наименование:</i> <b>{{ item.name }}</b>
        </li>
      </ul>
    </div>

    <div class="card-body">
      <div class="form-group">
          <div style="background-color: #2c3e50"> Профессия: {{ empl.professions }}</div>
          <select v-model="empl.professions">
            <option disabled value="">Выберете профессию</option>
            <option v-for="(item, index) in prof_list"
                    :key="index"
                    class="list-group-item">
              {{item.id}}
            </option>

          </select>
        <br>
        <br>
        <br>
        <br>
      </div>
      <form>
        <div class="form-group">
          <label htmlFor="name">ФИО</label>
          <br/>
          <input
              v-model="empl.fio"
              type="text"
              class="form-control"
              id="fio"
              name="fio"/>
          <br/>
          <br/>
        </div>
        <div class="form-group">
          <label htmlFor="name">Примечание</label>
          <br/>
          <input
              v-model="empl.description"
              type="text"
              class="form-control"
              id="description"
              name="description"/>
          <br/>
          <br/>
        </div>
        <div class="form-group">
          <button
              @click="handleSave()"
              :disabled="isSaving"
              type="button"
              class="btn btn-outline-primary mt-3">
            Создать
          </button>
        </div>
      </form>
    </div>
  </div>

</template>

