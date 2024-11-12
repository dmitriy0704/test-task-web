<script>
    import axios from 'axios'


    export default {
      name: "App",
      data() {
        return {
          answer: {},
        };
      },
      methods: {
        async getBitcoinIndex() {
          const { data } = await axios.get(
              "http://localhost:8080/api/dept?list",
          );
          this.answer = data;
        },
      },
      beforeMount() {
        this.getBitcoinIndex();
      },
    };
</script>

<template>
    <div class="row">
        <div class="col-md-12">
            <h3 class="green">Все департаменты</h3>
        </div>
        <div class="col-md-6">
          {{ answer }}

<!--            <ul class="list-group">-->
<!--                <li v-for="(item, index) in catFacts" :key="index" class="list-group-item">{{index + 1}}. {{item.name}}</li>-->
<!--            </ul>-->
        </div>
        <div class="col-md-12 text-center">
                <button @click="loadMoreFacts" class="btn btn-md btn-primary">{{ fetchingFacts ? '...' : 'Load more' }}</button>
        </div>
    </div>
</template>


