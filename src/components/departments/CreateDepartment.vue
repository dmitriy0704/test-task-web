<script >
import axios from 'axios'

export default {
  name: 'CreateDepartment',
  components: {},
  data() {
    return {
      dept: {
        name: '',
        description: ''
      },
      isSaving:false,
    };
  },
  methods: {
    handleSave() {
      this.isSaving = true
      axios.post('http://localhost:8080/api/dept', this.dept)
          .then(response => {
            this.isSaving = false
            this.dept.name = ""
            this.dept.description = ""
            return response
          })
          .catch(error => {});
    },
  },
};
</script>

<template>

  <div class="col-md-12">
    <h3 class="green">Создание отдела</h3>
  </div>
    <div class="card">

      <div class="card-body">
        <form>
          <div class="form-group">
            <label htmlFor="name">Наименование</label>
            <br/>

            <input
                v-model="dept.name"
                type="text"
                class="form-control"
                id="name"
                name="name"/>
            <br/>
            <br/>
          </div>

          <div class="form-group">
            <label htmlFor="name">Примечание</label>
            <br/>

            <input
                v-model="dept.description"
                type="text"
                class="form-control"
                id="description"
                name="description"/>
            <br/>
            <br/>
          </div>

          <button
              @click="handleSave()"
              :disabled="isSaving"
              type="button"
              class="btn btn-outline-primary mt-3">
            Создать
          </button>
        </form>
      </div>
    </div>

</template>