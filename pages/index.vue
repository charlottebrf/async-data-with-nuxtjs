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
  data() {
    return { myQuote: 'placeholder'}
  },
   async asyncData()  {
    try {
      let response = await axios.get("https://type.fit/api/quotes")
      
      if (response.status !== 200) {
        throw new Error('Could not fetch quotes')
      }

      let text =  await response.data;
      return { myQuote: text }

    } catch(e) {
      console.log('Here is the error', e)
    }
  },
});

</script>