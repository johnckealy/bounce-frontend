<template>
    <div class="tile is-7 is-parent">
      <div class="map_box tile is-parent">
        <div class="tile is-11 is-child box has-ribbon">
          <div class="ribbon is-large is-dark">Bounce Map Demo</div>
          <div class="image is-square">
            <div id='map'></div>
          </div>
        </div>
      </div>
    </div>
</template>


<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "Mapbox",
  head: {
    link: [
      {
        rel: "stylesheet",
        href: "https://api.mapbox.com/mapbox-gl-js/v1.9.1/mapbox-gl.css",
      },
    ],
  },
  data() {
    return {
      mapboxToken: "pk.eyJ1IjoiY2ZhaGxncmVuMSIsImEiOiJjazdiZWtqaDEwMDhyM2xvNTJoZDFxcjFqIn0.Chg6D1kZntCd3Gt3d0HxpA"
    };
  },
  mounted() {
    this.createmap();
  },
  methods: {
    createmap() {
      mapboxgl.accessToken = this.mapboxToken
      
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/cfahlgren1/cjwhv3k951qzw1cs0q5ukvtxi",
        center: [-122.431297, 37.773972],
        zoom: 11,
      });

      const map = this.map;

      map.on("load", function () {
        // Add a new source from our GeoJSON data and
        // set the 'cluster' option to true. GL-JS will
        // add the point_count property to your source data.
        map.addSource("courts", {
          type: "geojson",
          // Point to GeoJSON data. This example visualizes all M1.0+ earthquakes
          // from 12/22/15 to 1/21/16 as logged by USGS' Earthquake hazards program.
          data:
            "https://gist.githubusercontent.com/cfahlgren1/0e36f85d14138b9298a3f20a06d0050e/raw/38b4102fa593133c0a2b74312cd5177b0fbd1039/courts.geojson",
          cluster: true,
          clusterMaxZoom: 14, // Max zoom to cluster points on
          clusterRadius: 50, // Radius of each cluster when clustering points (defaults to 50)
        });

        map.addLayer({
          id: "clusters",
          type: "circle",
          source: "courts",
          filter: ["has", "point_count"],
          paint: {
            // Use step expressions (https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-step)
            // with three steps to implement three types of circles:
            //   * Blue, 20px circles when point count is less than 100
            //   * Yellow, 30px circles when point count is between 100 and 750
            //   * Pink, 40px circles when point count is greater than or equal to 750
            "circle-color": [
              "step",
              ["get", "point_count"],
              "#FF9B71",
              100,
              "#f1f075",
              750,
              "#f28cb1",
            ],
            "circle-radius": [
              "step",
              ["get", "point_count"],
              20,
              100,
              30,
              750,
              40,
            ],
          },
        });

        map.addLayer({
          id: "cluster-count",
          type: "symbol",
          source: "courts",
          filter: ["has", "point_count"],
          layout: {
            "text-field": "{point_count_abbreviated}",
            "text-font": ["DIN Offc Pro Medium", "Arial Unicode MS Bold"],
            "text-size": 12,
          },
        });

        map.addLayer({
          id: "unclustered-point",
          type: "circle",
          source: "courts",
          filter: ["!", ["has", "point_count"]],
          paint: {
            "circle-color": "#11b4da",
            "circle-radius": 8,
            "circle-stroke-width": 1,
            "circle-stroke-color": "#fff",
          },
        });

        // inspect a cluster on click
        map.on("click", "clusters", function (e) {
          var features = map.queryRenderedFeatures(e.point, {
            layers: ["clusters"],
          });
          var clusterId = features[0].properties.cluster_id;
          map
            .getSource("courts")
            .getClusterExpansionZoom(clusterId, function (err, zoom) {
              if (err) return;

              map.easeTo({
                center: features[0].geometry.coordinates,
                zoom: zoom,
              });
            });
        });

        map.on("mouseenter", "clusters", function () {
          map.getCanvas().style.cursor = "pointer";
        });
        map.on("mouseleave", "clusters", function () {
          map.getCanvas().style.cursor = "";
        });
      });
      document.addEventListener("DOMContentLoaded", () => {
        // Get all "navbar-burger" elements
        const $navbarBurgers = Array.prototype.slice.call(
          document.querySelectorAll(".navbar-burger"),
          0
        );
        // Check if there are any navbar burgers
        if ($navbarBurgers.length > 0) {
          // Add a click event on each of them
          $navbarBurgers.forEach((el) => {
            el.addEventListener("click", () => {
              // Get the target from the "data-target" attribute
              const target = el.dataset.target;
              const $target = document.getElementById(target);

              // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
              el.classList.toggle("is-active");
              $target.classList.toggle("is-active");
            });
          });
        }
      });
    },
  },
};
</script>






<style>

#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
p {
  font-size: 19px;
}
li {
  font-size: 19px;
}
ul {
  font-size: 19px;
}
@-webkit-keyframes spinAround {
  from {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  to {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes spinAround {
  from {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  to {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.has-ribbon {
  position: relative;
}
.has-ribbon-left {
  position: relative;
}
.has-ribbon-left .ribbon {
  right: auto;
  left: 0;
  border-left: none;
  border-right: 0.1rem solid #dbdbdb;
}
.has-ribbon-bottom {
  position: relative;
}
.has-ribbon-bottom .ribbon {
  top: auto;
  bottom: 0.5em;
}
.ribbon {
  background-color: #fff;
  border: 0.1rem solid #dbdbdb;
  border-right: none;
  color: #363636;
  font-size: 1rem;
  justify-content: center;
  padding-left: 0.75em;
  padding-right: 0.75em;
  text-align: center;
  white-space: nowrap;
  position: absolute;
  top: 0.5em;
  right: 0;
  font-weight: 400;
  z-index: 2;
}
.ribbon.is-white:not(.is-outlined) {
  background-color: #fff;
  border-color: transparent;
  color: #0a0a0a !important;
}
.ribbon.is-white.is-outlined {
  background-color: transparent;
  border-color: #fff;
}
.ribbon.is-black:not(.is-outlined) {
  background-color: #0a0a0a;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-black.is-outlined {
  background-color: transparent;
  border-color: #0a0a0a;
}
.ribbon.is-light:not(.is-outlined) {
  background-color: #f5f5f5;
  border-color: transparent;
  color: #363636 !important;
}
.ribbon.is-light.is-outlined {
  background-color: transparent;
  border-color: #f5f5f5;
}
.ribbon.is-dark:not(.is-outlined) {
  background-color: #363636;
  border-color: transparent;
  color: #f5f5f5 !important;
}
.ribbon.is-dark.is-outlined {
  background-color: transparent;
  border-color: #363636;
}
.ribbon.is-primary:not(.is-outlined) {
  background-color: #00d1b2;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-primary.is-outlined {
  background-color: transparent;
  border-color: #00d1b2;
}
.ribbon.is-link:not(.is-outlined) {
  background-color: #3273dc;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-link.is-outlined {
  background-color: transparent;
  border-color: #3273dc;
}
.ribbon.is-info:not(.is-outlined) {
  background-color: #209cee;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-info.is-outlined {
  background-color: transparent;
  border-color: #209cee;
}
.ribbon.is-success:not(.is-outlined) {
  background-color: #23d160;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-success.is-outlined {
  background-color: transparent;
  border-color: #23d160;
}
.ribbon.is-warning:not(.is-outlined) {
  background-color: #ffdd57;
  border-color: transparent;
  color: rgba(0, 0, 0, 0.7) !important;
}
.ribbon.is-warning.is-outlined {
  background-color: transparent;
  border-color: #ffdd57;
}
.ribbon.is-danger:not(.is-outlined) {
  background-color: #ff3860;
  border-color: transparent;
  color: #fff !important;
}
.ribbon.is-danger.is-outlined {
  background-color: transparent;
  border-color: #ff3860;
}
.ribbon.is-small {
  font-size: 0.75rem;
}
.ribbon.is-medium {
  font-size: 1.25rem;
}
.ribbon.is-large {
  font-size: 1.5rem;
}
.ribbon.is-outlined {
  background-color: transparent;
}
</style>
