<template>
  <div>
  <p> Here is a quote</p>
  {{ this.myQuote }}
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios';

export default Vue.extend({
   async asyncData(context)  {
    try {
      // console.log('here is context', context)
      let response = await axios.get("https://type.fit/api/quotes")
      
      if (response.status !== 200) {
        throw new Error('Could not fetch quotes')
      }

      let text =  await response.data;
      // sets the value of the data object => this.myQuote = text no longer works now using asyncData rather than fetch with Vue lifecyclen hooks
      return { myQuote: text }

    } catch(e) {
      console.log('Here is the error', e)
    }
  },
});

</script>