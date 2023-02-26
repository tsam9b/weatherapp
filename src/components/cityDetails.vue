<template>
   <div class="modall-backdrop">
      <div class="modall"
        role="dialog"
        aria-labelledby="modallTitle"
        aria-describedby="modallDescription"
      >
        <header
          class="modall-header"
          id="modallTitle"
        >
        
          <slot name="header">
           
            <table id="modal-list-view" class="table_left">
              <tr>
                <td class="mtitle">  {{cityTitle}}</td>
                <td class="stitle">  ({{weatherDetails}}) </td>
                <td> <img :src="weatherDetailsIcon"/></td>
              </tr>
              
            </table>
           
          </slot>
          
          <button
            type="button"
            class="btn-close"
            @click="close"
            aria-label="Close modall"
          >
            x
          </button>
        </header>

        <section
          class="modall-body"
          id="modallDescription"
        >
          <slot name="body">

            <table id="list-view" class="table_left">
              <tr>
                <td> Temp: {{tmp}}</td>
              </tr>
              <tr>
                <td> Feel's like: {{feels_like}}</td>
              </tr>
              <tr>
                <td> Min temp: {{temp_min}}</td>
              </tr>
              <tr>
                <td> Max temp: {{temp_max}}</td>
              </tr>
              <tr>
                <td> Pressure: {{pressure}}</td>
              </tr>
          </table>
          <table id="list-view" class="table_right">
              <tr>
                <td> Sea level: {{sea_level}}</td>
              </tr>
              <tr>
                <td> Ground level: {{grnd_level}}</td>
              </tr>
              <tr>
                <td> Humidity: {{humidity}}</td>
              </tr>
              <tr>
                <td> Temp kf: {{temp_kf}}</td>
              </tr>
            </table>

          </slot>
        </section>

        <footer class="modall-footer">
          <slot name="footer">
          </slot>
          <button
            type="button"
            class="btn-green"
            @click="close"
            aria-label="Close modall"
          >
            Close
          </button>
        </footer>
      </div>
    </div>
</template>


<script>
export default {
  name: 'cityDetails',
  props:{
    cityTitle: String,
    weatherDetails: String,
    weatherDetailsIcon: String,
    tmp: Float32Array,
    feels_like: Float32Array,
    temp_min: Float32Array,
    temp_max: Float32Array,
    pressure: Float32Array,
    sea_level: Float32Array,
    grnd_level: Float32Array,
    humidity: Float32Array,
    temp_kf: Float32Array,

  },
  methods: {
    close() {
      this.$emit('close');
    },
  },
};
</script>

<style scoped> @import '../css/cityDetails.css';</style>