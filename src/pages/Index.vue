<template>
  <q-page class="bg-grey-9">
    
    <div class="row justify-center">
      <div class="col-6">
        <img alt="Quasar logo" src="~assets/mappurple.svg" />
      </div>
    </div>

    <div class="row justify-center">
      <div class="text-white col-10 text-center">
        <p>
          latitude: {{ lat }}
        </p>
        <p>
          longitude: {{ lng }}
        </p>
      </div>
    </div>

    <div class="row justify-center q-mt-lg">
      <q-btn @click="getLocation" size="lg" class="col-8" color="purple-6" label="Minha localização" push/>
    </div>
  
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",
  data() {
    return {
      lat: null,
      lng: null
    };
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        this.$q.loading.show();
        navigator.geolocation.getCurrentPosition(
          position => {
            this.lat = position.coords.latitude;
            this.lng = position.coords.longitude;
            this.$q.loading.hide();
            this.$q.notify({
              color: "positive",
              icon: "check",
              message: `Localização atualizada!`,
            });
          },
          error => {
            this.$q.loading.hide();
            this.$q.notify({
              color: "negative",
              message: `${error} Erro ao obter sua localização`
            });
          }
        );
      } else {
        console.log("Geolocation is not supported by this browser.");
      }
    }
  },
});
</script>
