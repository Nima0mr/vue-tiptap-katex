<template>
  <v-app>
    <vue-tiptap-katex
      ref="tiptap"
      :options="{ poem: true, reading: true, bubbleMenu: false, floatingMenu: false, persianKeyboard: true, mathliveOptions: { smartFence: true } }"
    />
<!--    <interactive-info-table></interactive-info-table>-->
    <v-btn @click="getContent">
      Get Content
    </v-btn>
    <hr>
    <div v-html="test" />
    <hr>
    <div
      ref="printdiv"
    >
      {{ test }}
    </div>
  </v-app>
</template>

<script>
import VueTiptapKatex from '@/vue-tiptap-katex';
export default {
  name: 'Test',
  components: {VueTiptapKatex },
  methods: {
    prepareForKatex () {
      let regex = /((\\\[((?! ).){1}((?!\$).)*?((?! ).){1}\\\])|(\$((?! ).){1}((?!\$).)*?((?! ).){1}\$))/gms;
      this.test = this.test.replace(regex, (match) => {
        return ' ' + match + ' '
      })
    },
    getContent () {
      this.test = this.$refs.tiptap.getContent()
      this.prepareForKatex()
    }
  },
  data () {
    return {
      test: '$\\begin{array}{cc}f(x) = a(x - 1)(x - 2) \\\\\\Rightarrow f(0) = a( - 1)( - 2) = 4\\\\\\\\\\Rightarrow 2a = 4 \\\\\\Rightarrow a = 2\\\\\\\\f(x) = 2(x - 1)(x - 2) \\\\\\Rightarrow f(3) = 2(2)(1) = 4\\end{array}$'
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$refs.tiptap.setContent(this.test)
    })
  }
}
</script>

<style>

.katex {
  direction: ltr;
}
  .beit {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
  }
  .beit .mesra {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
    -ms-flex-preferred-size: 0;
    flex-basis: 0;
    -webkit-box-flex: 1;
    -ms-flex-positive: 1;
    flex-grow: 1;
    max-width: 100%;
    white-space: nowrap;
  }

  @media only screen and (max-width: 500px) {
    .beit {
      flex-direction: column;
    }
    .beit .mesra {
      white-space: normal;
      flex-basis: auto;
    }
  }
</style>
