<script >
import {ref, onMounted} from 'vue'
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  name: 'CreateProfession',
  components: {},
  data() {
    return {
      prof: {
        name: '',
        description: ''
      },
      isSaving:false,
    };
  },
  methods: {
    handleSave() {
      this.isSaving = true
      axios.post('http://localhost:8080/api/prof', this.prof)
          .then(response => {
            this.isSaving = false
            this.prof.name = ""
            this.prof.description = ""
            return response
          })
          .catch(error => {});
    },
  },
};
</script>

<template>

  <div class="col-md-12">
    <h3 class="green">Создать профессию</h3>
  </div>
    <div class="card">

      <div class="card-body">
        <form>
          <div class="form-group">
            <label htmlFor="name">Наименование</label>
            <br/>

            <input
                v-model="prof.name"
                type="text"
                class="form-control"
                id="name"
                name="name"/>
            <br/>
            <br/>
          </div>
          <div class="form-group">
            <label htmlFor="">Примечание</label>
            <br/>

            <input
                v-model="prof.description"
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