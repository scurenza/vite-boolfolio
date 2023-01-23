<script>
import { store } from '../store';

export default {
    name: 'ProjectCard',
    data() {
        return {
            contentMaxLength: 100,
            store,
        }
    },
    props: {
        project: Object,
    },
    computed: {
        contentPreview() {
            if (this.project.content && this.project.content.length > this.contentMaxLength) {
                return this.project.content.substr(0, this.contentMaxLength) + '...';
            }
            return this.project.content;
        }
    },
    methods: {
        // truncateText(text) {
        //     if (text && text.length > this.contentMaxLength) {
        //         return text.substr(0, this.contentMaxLength) + '...';
        //     }
        //     return text;
        // }
    }
}
</script>

<template>
    <div class="card mb-3">
        <div class="card-body">
            <div class="row justify-content-between">
                <div class="col-4">
                    <img v-if="project.cover_image" class="w-100" :src="`${this.store.apiBaseUrl}/storage/${project.cover_image}`" alt="">
                    <div v-else>
                        Nessuna immagine
                    </div>
                </div>
                <div class="col-7">
                    <h3 class="card-title">{{ project.title }}</h3>
                    <div class="d-flex justify-content-between">
                        <p>
                            <span v-for="technology in project.technologies" :key="technology.id"> #{{ technology.name }} </span>

                        </p>
                        <p class="text-end text-success">{{ project.type ? project.type.name : 'Nessuna tipologia' }}
                        </p>
                    </div>
                    <p class="card-text">
                        {{ contentPreview }}
                    </p>
                    <!-- <a class="btn btn-primary" href="">Leggi</a> -->
                    <router-link :to="{ name: 'single-project', params: { slug: project.slug } }" class="btn btn-primary" href="">
                        Leggi
                    </router-link>
                </div>
            </div>

        </div>
    </div>
</template>