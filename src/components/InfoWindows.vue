<template lang="html">
  <div class="info-windows">
    <google-map id="map" ref="Map">
      <google-map-marker
        :key="index"
        v-for="(infowindow, index) in infoWindowsList"
        :position="infowindow.position"
        @click="toggleInfoWindow(infowindow)"
      ></google-map-marker>
      <google-map-infowindow
              v-for="(infowindow, index) in infoWindowsList"
              :key="`info-window-${index}`"
              :position="infowindow.position"
              :show.sync="showInfo"
              :options="{maxWidth: 300}"
              @info-window-clicked="infoClicked($event, infowindow)"
      >
        <h4 >{{infoWIndowContext.title}}</h4>
        <p>{{infoWIndowContext.description}}</p>
      </google-map-infowindow>
    </google-map>
  </div>
</template>

<script>
import cities from '../assets/cities.json'
export default {
  data () {
    return {
      showInfo: true,
      infoWIndowContext: {
        title: 'Hello world',
        description: 'Description',
        position: {
          lat: 44.2899,
          lng: 11.8774
        }
      },
      infoWindowsList: cities
    }
  },
  methods: {
    toggleInfoWindow (context) {
      this.infoWIndowContext = context
      this.showInfo = true
    },
    infoClicked(context, spot) {
      console.log(context, spot)
    }
  }
}
</script>
