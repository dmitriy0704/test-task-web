<script >
import {ref, onMounted} from 'vue'
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  name: 'CreateDept',
  components: {},
  data() {
    return {
      dept: {
        name: '',
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
            <label htmlFor="name">Название</label>
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