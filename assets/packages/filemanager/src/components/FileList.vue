<template>
  <div :class="'col-md-'+cols">
    <div class="ls-flex ls-flex-row align-items-flex-end align-content-flex-end ls-space margin bottom-10">
      <div class="btn-group" role="group">
        <button type="button" id="FileManager--change-filewiz-to-tablerep" class="btn" @click="fileviz='tablerep'" :class="fileviz=='tablerep' ? 'btn-info active' : 'btn-default'">Table</button>
        <button type="button" id="FileManager--change-filewiz-to-iconrep" class="btn" @click="fileviz='iconrep'" :class="fileviz=='iconrep' ? 'btn-info active' : 'btn-default'">Icons</button>
      </div>
    </div>
    <div class="container-fluid">
        <component :is="fileviz" @setLoading="setLoading" :loading="loading"></component>
    </div>
    <modals-container />
  </div>
</template>

<script>
import Tablerep from './subcomponents/_tableRepresentation';
import Iconrep from './subcomponents/_iconRepresentation';

import applyLoader from '../mixins/applyLoader';

export default {
  name: 'FileList',
  mixins: [applyLoader],
  components: {
    Tablerep,
    Iconrep
  },
  props: {
    cols: {type: Number, default: 6},
  },
  data() {
    return {
      event: null
    };
  },
  computed: {
        fileviz: {
            get() { return this.$store.state.fileRepresentation; },
            set(nV) {this.$store.commit('setFileRepresentation', nV);}
        }
  }
}
</script>

<style lang="scss" scoped>
    .scoped-loadingOverlay {
        position: absolute;
        top: 0;
        left: 0;
        width:98%;
        height:98%;
        margin: 1%;
        padding:1%;
        background: hsla(0,0%,75%,0.5);
        z-index: 2;
    }
</style>
