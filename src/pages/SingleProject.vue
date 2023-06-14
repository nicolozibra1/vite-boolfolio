<template>
    <div class="loader d-flex justify-content-center align-items-center">
        <LoadingComponent v-if="store.loading"/>
    </div>
    <div v-if="project">
        <h1>{{ project.title }}</h1>
        <img :src="project.image" :alt="project.title">
        <ul>
            <li v-for="technology in project.technologies">
                {{ technology.name }}
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
import LoadingComponent from '../components/LoadingComponent.vue';
import { store } from '../data/store.js';
    export default {
        name: 'SingleProject',
        components: {
            LoadingComponent
        },
        data() {
            return {
                store,
                project: null,
            }
        },
        methods: {
            getProject() {
                store.loading = true;
                axios.get(`${store.apiUrl}/projects/${this.$route.params.slug}`).then((res) =>{
                    if(res.data.success) {
                        this.project = res.data.results;
                    }
                    else {
                        this.$router.push({name: 'not-found'})
                    }
                }).finally(() => {
                    store.loading = false;
                })
            }
        },
        mounted() {
            this.$router;
            this.$route;
            this.getProject();
        }
    }
</script>

<style lang="scss" scoped>

</style>