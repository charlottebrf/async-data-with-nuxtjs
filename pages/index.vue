<template>
  <div>
  <p> Here is a quote</p>
  {{ this.myQuote }}
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return { myQuote: 'placeholder'}
  },

   created() {
     this.gettingQuotes()
   },
    methods: {
    gettingQuotes: async function() {
    try {
      let response = await fetch("https://type.fit/api/quotes")
      if (!response.ok) {
        throw new Error('Could not fetch quotes')
      }

      let text =  await response.text();
      this.myQuote = text;

    } catch(e) {
      console.log('Here is the error', e)
    }
  }
}
});

</script>