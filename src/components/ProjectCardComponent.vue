<template>
    <div class="col">
              <div class="card" style="width:200px">
                  <div class="card-title">
                      <h3>{{ project.title }}</h3>
                  </div>
                  <div class="card-img-top">
                      <img :src="getImagePath" :alt="project.title" class="img-fluid">
                  </div>
                  <div class="card-body">
                      <h6>{{ project.type.name }}</h6>
                      <div class="box-badge" v-for="(technology, index) in project.technologies">
                        <span class="badge text-bg-warning">{{ technology.name }}</span>
                      </div>
                      <router-link :to="{ name: 'single-project', params:{slug: project.slug} }" class="btn btn-primary">
                        more details
                      </router-link>
                  </div>
              </div>
          </div>
</template>

<script>
    export default {
        name: 'ProjectCardComponent',
        props: ['project'],
        data() {
            return {

            }
        },
        computed: {
            getImagePath() {
                return this.project.image
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>