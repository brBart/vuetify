<template>
  <div :id="id"><!-- Ad --></div>
</template>

<script>
  export default {
    props: {
      id: {
        type: String,
        default: undefined
      },
      scriptId: {
        type: String,
        default: undefined
      },
      src: {
        type: String,
        default: undefined
      }
    },

    data: () => ({
      timeout: null
    }),

    watch: {
      '$route.path': 'serve'
    },

    mounted () {
      if (!this.src) return

      clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {
        const script = document.createElement('script')
        script.type = 'text/javascript'
        script.src = this.src

        if (this.scriptId) script.id = this.scriptId

        if (this.$el) this.$el.append(script)
        else console.warn('%cPlease consider allowing ads, we\'ve gotta eat too :(', 'font-size: 24px')
      }, 300)
    },

    methods: {
      serve: () => {} /* noop */
    }
  }
</script>
