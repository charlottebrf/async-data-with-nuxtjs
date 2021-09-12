<template>
  <div>
  <p> Here is a quote</p>
  {{ this.myQuote }}
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
   async asyncData({ $axios })  {
    try {
     // using $axios.$get means you just get the data back, rather
      let response = await $axios.$get()
      
      // We can no longer do this because we only get back the data object not the full response object as previously from axios
      // if (response.status !== 200) {
      //   throw new Error('Could not fetch quotes')
      // }

      // sets the value of the data object => this.myQuote = text no longer works now using asyncData rather than fetch with Vue lifecyclen hooks
      return { myQuote: response }

    } catch(e) {
      console.log('Here is the error', e)
    }
  },
});

</script>