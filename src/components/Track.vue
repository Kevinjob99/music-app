<template>
  <div class="card" v-if="track && track.album">
    <div class="card-image">
      <figure class="image is-1by1">
        <img v-bind:src="track.album.images[0].url">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img v-bind:src="track.album.images[0].url">
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-6">
            <strong>{{track.name}}</strong>
          </p>
          <p class="subtitle is-6">{{track.artists[0].name}}</p>
        </div>
      </div>
      <div class="content">
        <nav class="level">
          <div class="level-left">
            <button class="level-item button bg">
              <small class="mr">{{track.duration_ms | ms-to-mm}} Minutos</small>
              <small class="icon is-small mr" v-on:click="selectTrack">▶️</small>
              <small class="icon is-small" v-on:click="goToTrack(track.id)">🎵</small>
            </button>
          </div>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
import trackMixin from "../mixins/track";

export default {
  mixins: [trackMixin],

  props: {
    track: { type: Object, required: true }
  },

  methods: {
    goToTrack(id) {
      if (!this.track.preview_url) {
        return;
      }
      this.$router.push({
        name: "track",
        params: { id }
      });
    }
  }
};
</script>

<style lang="scss">
.mr {
  margin-right: 25px;
}
.bg {
  background-color: #ff3861;
}
</style>