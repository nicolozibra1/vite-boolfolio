<template>
    <div class="container">
        <h1>{{ title }}</h1>
        <div class="row">
            <ProjectCardComponent v-for="(project, index) in projects" :key="project.id" :project="project"/>
            <nav aria-label="Page navigation example">
                <ul class="pagination">
                    <li class="page-item"><button class="page-link" @click="getData(currentPage - 1)">Previous</button></li>
                    <li class="page-item" v-for="n in lastPage"><button class="page-link" @click="getData(n)">{{ n }}</button>
                    </li>
                    <li class="page-item"><button class="page-link" @click="getData(currentPage + 1)">Next</button></li>
                </ul>
            </nav>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ProjectCardComponent from '../components/ProjectCardComponent.vue';
export default {
  'name': 'ProjectList',
  components: {
    ProjectCardComponent
  },
  data() {
      return {
          title: 'Portfolio',
          projects: [],
          apiUrl: 'http://127.0.0.1:8000/api',
          currentPage: 1,
          lastPage: null,
      }
  },
  methods: {
      getData(numPage) {
          axios.get(`${this.apiUrl}/projects`, {
              params: {
                  'page': numPage
              }
          }).then((res) => {
              console.log(res);
              this.projects = res.data.results.data;
              this.currentPage = res.data.results.current_page;
              this.lastPage = res.data.results.last_page;
          })
      }
  },
  mounted() {
      this.getData(1);
  }

}
</script>

<style lang="scss" scoped>

</style>