<template>
    <div>
        <div v-if="post">
            <h2 class="text-center">{{ post.title }}</h2>
            <img v-if="post.thumb" class="img-fluid" :src="post.thumb" alt="Foto Vacanza">
            <h6 class="fs-4">{{ post.subtitle }}</h6>
            <p class="fs-5 lh-base py-3">{{ post.description }}</p>
            <p class="fw-light fs-6">{{ post.dailyJournal }}</p>
            <div>
                <!-- Passa le coordinate -->
                <Map :locations="getLocations()" />
            </div>
        </div>
        <div v-else>
            <p>Nessun post disponibile.</p>
        </div>
    </div>
</template>

<script>
import Map from './Map.vue';

export default {
    name: 'AppPost',
    components: {
        Map
    },
    props: {
        post: {
            type: Object,
            required: true
        }
    },
    methods: {
        getLocations() {
            return [
                {
                    popup: this.post.popup,
                    latitude: this.post.latitude, 
                    longitude: this.post.longitude
                }
            ];
        }
    }
}
</script>

<style lang="scss" scoped>
img {
    width: 500px;
    padding: 20px 0;
}
</style>
