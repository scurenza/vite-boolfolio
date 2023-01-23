<script>
import axios from 'axios';
import { store } from "../store";

export default {
    name: "SingleProject",
    data() {
        return {
            store,
            project: {}
        }
    },
    created() {
        const slug = this.$route.params.slug;
        axios.get(`${this.store.apiBaseUrl}/api/projects/${slug}`).then(resp => {
            if (resp.data.success) {
                // Caso del project trovato
                this.project = resp.data.project;
            } else {
                // project non trovato => reindirizzo nella pagina not found
                this.$router.push({ name: "not-found" });
            }
        });
    },
    computed: {
        type() {
            return this.project.type ? this.project.type.name : 'Nessuna tipologia';
        }
    }
}
</script>

<template>
    <main>
        <div class="container">
            <h1 class="mt-3 text-center">{{ project.title }}</h1>
            <h5 class="text-center mt-2 text-uppercase text-primary">{{ type }}</h5>
            <img v-if="project.cover_image" :src="`${store.apiBaseUrl}/storage/${project.cover_image}`" alt="">
            <div v-else class="text-center mt-4">Nessuna immagine</div>

            <p>{{ project.content }}</p>
        </div>
    </main>
</template>