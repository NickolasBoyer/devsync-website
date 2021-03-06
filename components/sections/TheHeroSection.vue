<template lang="pug">
  section.section.section--full.section-hero#hero
    .section__body
      h1.section-hero__title#hero-title Visually edit CSS and live-sync the result with your code editor.
      h2.section__sub-title.section-hero__sub-title Design quicker. Edit your CSS without writing CSS. Devsync finds your CSS and edits it through your editor. Live.
      .m-2
        button.section-hero__button.section-hero__button--bounce( @click="toggleDemo" :disabled="buttonDisabled" ) {{ demoActive ? 'Deactivate Demo' : 'Try Live Demo' }}
        button.section-hero__button.section-hero__button--sec( @click="goToInfo" ) Read more
      p.section-hero__sub-text 30-Day Money-Back Guarantee
    img.section-hero__browser-img( src="img/browser-preview.webp" alt="Browser preview" onerror="this.onerror=null; this.src='img/browser-preview.png'" )
    img.section-hero__editor-img( src="img/editor-preview.webp" alt="Editor preview" onerror="this.onerror=null; this.src='img/editor-preview.png'" )
</template>

<script>

const particleConfig = {
  "particles": {
    "number": {
      "value": 40,
      "density": {
        "enable": true,
        "value_area": 800
      }
    },
    "color": {
      "value": "#999"
    },
    "shape": {
      "type": "circle",
      "stroke": {
        "width": 0,
        "color": "#000000"
      },
      "polygon": {
        "nb_sides": 5
      },
      "image": {
        "src": "img/github.svg",
        "width": 100,
        "height": 100
      }
    },
    "opacity": {
      "value": 0.4,
      "random": false,
      "anim": {
        "enable": false,
        "speed": 1,
        "opacity_min": 0.1,
        "sync": false
      }
    },
    "size": {
      "value": 3,
      "random": true,
      "anim": {
        "enable": false,
        "speed": 40,
        "size_min": 0.1,
        "sync": false
      }
    },
    "line_linked": {
      "enable": true,
      "distance": 150,
      "color": "#ffffff",
      "opacity": 0.1,
      "width": 1
    },
    "move": {
      "enable": true,
      "speed": 1,
      "direction": "none",
      "random": false,
      "straight": false,
      "out_mode": "out",
      "bounce": false,
      "attract": {
        "enable": false,
        "rotateX": 600,
        "rotateY": 1200
      }
    }
  },
  "retina_detect": true
}

export default {
  props: {
    demoActive: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      buttonDisabled: true
    }
  },
  mounted () {
    require('particles.js')
    window.particlesJS('hero', particleConfig)
    window.addEventListener('load', () => { this.buttonDisabled = false }, { once: true })
  },
  methods: {
    toggleDemo() {
      this.$emit('toggleDemo')
      this.demoActive ? sa("deactivate_demo") : sa("activate_demo")
    },
    goToInfo() {
      document.getElementById('info').scrollIntoView({ behavior: 'smooth' })
      if (this.demoActive) this.$emit('toggleDemo')
      sa("go_to_info")
    }
  }
}
</script>

<style lang="sass" scoped>
.section-hero

  &__title
    @apply max-w-4xl font-bold m-1
    font-size: 3.2rem
    line-height: 1em // Tailwind doesn't provide unit, is annoying for demo
    // font-family: 'SF Pro Display', 'Arial', sans-serif

  &__sub-title
    @apply max-w-2xl
  
  &__button
    @apply py-2 px-8 m-1 text-gray-100 text-2xl font-bold
    border-radius: 5px
    background-image: linear-gradient(149deg, #588BFFDD 0%, #B745F2DD 98%)
    transition: transform .3s ease-out

    &:disabled, &[disabled]
      filter: grayscale(1)
      cursor: wait

    &:hover
      transform: scale(1.05)

    &--sec
      background-image: none
      // box-shadow: inset 0 0 0 3px #cbd5e0 // inset border

    &--bounce
      animation-name: bounce
      animation-duration: 2s
      animation-iteration-count: infinite
      animation-direction: alternate

  &__sub-text
    @apply text-sm font-light text-gray-400 m-1

  &__browser-img
    @apply absolute object-contain
    height: 80%
    top: 10%
    left: 0
    transform: translateX(calc(-100% + 18vw))
    z-index: -1

    @media (max-width: 920px)
      display: none

  &__editor-img
    @apply absolute object-contain
    height: 80%
    top: 10%
    right: 0
    transform: translateX(calc(100% - 18vw))
    z-index: -1

    @media (max-width: 920px)
      display: none

@keyframes bounce
  0%
    transform: scale(1)
  50%
    transform: scale(1.03)
  100%
    transform: scale(1)
</style>