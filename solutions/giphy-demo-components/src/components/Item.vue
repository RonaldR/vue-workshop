<template>
  <div class="item image">
    <img v-if="result.images.downsized_medium" v-bind:src="result.images.downsized_medium.url" data-action="zoom" />
    <span class="info">
      <span class="title">{{ result.title }}</span>
    </span>
  </div>
</template>

<script>
export default {
  name: 'item',
  props: ['result'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .image {
    position: relative;
  }

  .image img {
    display: flex;
    height: 100%;
    width: 100%;
    object-fit: cover;
    border-radius: 5px;
  }

  .info {
    padding: 15px;
    position: absolute;
    bottom: 0;
    right: 0;
    max-width: 80%;
    font-size: 14px;
    text-align: right;
    color: #fff;
    text-shadow: 1px 0px 1px #252525;
  }

  .maker {
    display: block;
    font-weight: bold;
  }

  img[data-action="zoom"] {
    cursor: pointer;
    cursor: -webkit-zoom-in;
    cursor: -moz-zoom-in;
  }

  .zoom-img,
  .zoom-img-wrap {
    position: relative;
    z-index: 666;
    transition: all 300ms;
  }

  img.zoom-img {
    cursor: pointer;
    cursor: -webkit-zoom-out;
    cursor: -moz-zoom-out;
  }

  .zoom-overlay {
    z-index: 420;
    background: #fff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    filter: 'alpha(opacity=0)';
    opacity: 0;
    transition: opacity 300ms;
  }

  .zoom-overlay-open .zoom-overlay {
    filter: 'alpha(opacity=100)';
    opacity: 1;
  }

  .zoom-overlay-open,
  .zoom-overlay-transitioning {
    cursor: default;
  }
</style>
