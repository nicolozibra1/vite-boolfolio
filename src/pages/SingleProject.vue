<template>
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
    export default {
        name: 'SingleProject',
        data() {
            return {
                project: null,
                apiUrl: 'http://127.0.0.1:8000/api',
            }
        },
        methods: {
            getProject() {
                axios.get(`${this.apiUrl}/projects/${this.$route.params.slug}`).then((res) =>{
                    if(res.data.success) {
                        this.project = res.data.results;
                    }
                    else {
                        this.$router.push({name: 'not-found'})
                    }
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