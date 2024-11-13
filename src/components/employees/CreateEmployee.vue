<script>
import axios from 'axios'
import { ref } from 'vue'

export default {
  name: 'CreateEmployee',
  components: {},
  data() {
    return {

      prof_list: {},
      employee: {
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
      axios.post('http://localhost:8080/api/empl', this.employee)
          .then(response => {
            this.isSaving = false
            this.employee.fio = ""
            this.employee.description = ""
            // this.empl.profession = ""
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
  <div class="form">

      <form>

        <div class="form-group">
          <label htmlFor="name">ФИО</label>
          <br/>
          <input
              v-model="employee.fio"
              type="text"
              class="form-control"
              id="fio"
              name="fio"/>
          <br/>
          <br/>
        </div>

        <div class="form-group">
          <div> Профессия: </div>
          <select v-model="employee.profession">
            <option disabled value="">Выберете профессию</option>
            <option v-for="(item, index) in prof_list"
                    :key="index"
                    class="list-group-item">
              {{item.name}}
            </option>
          </select>
          <input
              style="display: none"
              v-model="employee.profession"
              type="text"
              class="form-control"
              id="profession"
              name="profession"/>
          <br/>
          <br/>
        </div>


        <div class="form-group">
          <label htmlFor="name">Примечание</label>
          <br/>
          <input
              v-model="employee.description"
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

</template>

