
<template>
    <div>
        <!-- <label>
            AutoComplete
            <GmapAutocomplete :position.sync="markers[0].position" @keyup.enter="usePlace" @place_changed="setPlace">
            </GmapAutocomplete>
            <button @click="usePlace">Add</button>
        </label> -->


        <gmap-map
            :center="centers"
            :zoom="11"
            map-type-id="terrain"
            style="width: 100%; height: 340px"
        >
            <gmap-marker
                @dragend="updateMaker"
                :key="index"
                v-for="(m, index) in markers"
                :position="m.position"
                :clickable="true"
                :draggable="true"
                @click="centers=m.position"
            ></gmap-marker>
              <!-- @click="centers=m.position" -->
        </gmap-map>

    </div>
</template>

<script>

    export default {
        data() {
            return {
                centers: {lat: 39.90419989999999,lng: 116.4073963},
                markers: [{
                    position: {lat: 39.90419989999999,lng: 116.4073963}
                }],
                place: null,
            }
        },
        description: 'Autocomplete Example (#164)',
        mounted() {

        },
        methods: {
            setPlace(place) {
                this.place = place
            },
            setDescription(description) {
                this.description = description;
            },
            usePlace(place) {
                if (this.place) {
                    var newPostion = {
                        lat: this.place.geometry.location.lat(),
                        lng: this.place.geometry.location.lng(),
                    };
                    this.center = newPostion;
                    this.markers[0].position =  newPostion;
                    this.place = null;
                }
            },
            updateMaker: function(event) {
                console.log('updateMaker, ', event.latLng.lat());
                this.markers[0].position = {
                    lat: event.latLng.lat(),
                    lng: event.latLng.lng(),
                }
            },
        }
    }
</script>
