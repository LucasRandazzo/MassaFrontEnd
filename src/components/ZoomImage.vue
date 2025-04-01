<template>
    <div 
      class="zoom-container" 
      @mousemove="handleMouseMove" 
      @mouseleave="resetZoom"
    >
      <img :src="src" alt="Imagem com zoom" :style="imgStyle" />
    </div>
  </template>
  
  <script>
  export default {
    name: 'ZoomImage',
    props: ['src'],
    data() {
      return {
        originX: '50%',
        originY: '50%',
        zoom: false,
      };
    },
    computed: {
      imgStyle() {
        return {
          transform: this.zoom ? 'scale(3)' : 'scale(1)',
          transformOrigin: `${this.originX} ${this.originY}`,
          transition: 'transform 0.2s ease-out',
        };
      }
    },
    methods: {
      handleMouseMove(event) {
        const rect = event.currentTarget.getBoundingClientRect();
        const x = event.clientX - rect.left;
        const y = event.clientY - rect.top;
        const originX = (x / rect.width) * 100;
        const originY = (y / rect.height) * 100;
        this.originX = `${originX}%`;
        this.originY = `${originY}%`;
        this.zoom = true;
      },
      resetZoom() {
        this.zoom = false;
      }
    }
  };
  </script>
  
  <style scoped>
  .zoom-container {
    overflow: hidden;
    display: inline-block;
  }
  .zoom-container img {
    display: block;
    width: 100%;
    height: auto;
  }
  </style>
  