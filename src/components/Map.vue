<template>
    <div id="map" style="height: 500px; width: 100%;"></div>
</template>

<script>
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';
import markerIcon from 'leaflet/dist/images/marker-icon.png';
import markerShadow from 'leaflet/dist/images/marker-shadow.png';

export default {
    name: 'Map',
    props: {
        locations: {
            type: Array,
            required: true
        }
    },
    mounted() {
        this.initMap();
    },
    methods: {
        initMap() {
            const map = L.map('map');

            // Layer con le mappe di OpenStreetMap
            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: '&copy; el mejo'
            }).addTo(map);

            // Imposta manualmente l'icona del marker
            const defaultIcon = L.icon({
                iconUrl: markerIcon,
                shadowUrl: markerShadow
            });

            // Se ci sono coordinate, centrare la mappa
            if (this.locations.length) {
                const bounds = L.latLngBounds(this.locations.map(loc => [loc.latitude, loc.longitude]));
                map.fitBounds(bounds);

                this.locations.forEach(location => {
                    L.marker([location.latitude, location.longitude], {icon: defaultIcon}).addTo(map)
                        .bindPopup(location.popup)
                        .openPopup();
                });
            } else {
                // Vista di default se non ci sono coordinate
                map.setView([74.505, -20.09], 13);
            }
        }
    }
}
</script>

<style scoped></style>
