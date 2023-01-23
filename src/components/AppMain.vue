<script>
import axios from 'axios';
import AppLoader from './AppLoader.vue';
import ProjectCard from './ProjectCard.vue';
import { store } from '../store';

export default {
    name: 'AppMain',
    components: {  ProjectCard, AppLoader },
    data() {
        return {
            store,
            projects: [],
            loading: false
        };
    },
    created() {
        this.getProjects();
    },
    methods: {
        getProjects() {
            this.loading = true;
            axios.get(`${this.store.apiBaseUrl}/api/projects`).then(resp => {
                this.projects = resp.data.results;
                this.loading = false;
            });
        }
    }
}
</script>

<template>
    <div class="container">
        <h2 class="text-center mb-3">
            Tutti i progetti
        </h2>
        <AppLoader v-if="loading" />
        <div v-else class="row justify-content-center">
            <div class="col-10-col-md-9 col-lg-8">
                <ProjectCard :project="project" v-for="project in projects" :key="project.id" />
            </div>
        </div>
    </div>
</template>