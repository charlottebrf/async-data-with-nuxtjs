# Async Data notes

* Using `mounted` is a very common approach for handling async data. Make an async request inside the mounted fn so that the component is populated with data once the code has been executed.

```
data() {
    return {
        stuffToShow = [];
    }
},
mounted() {
    fetch('myapi')
    .then(response => {
        response.json().then(stuffBack => {
            this.stuffToShow = stuffBack
        })
    })
}
```

* Meta tags not set => because fetch happens once the page is loaded whilst head method runs before page is served => major drawback of using `mounted` in nuxt.js to fetch data. It is also not compatible with SSR.


# SSR
* When doing SSR need to fetch data on the server side. This way the data will be present when the page is served.

# Enter AsyncData
* asyncData works the same way with the data - it returns an object
* The object you return will be merged with the data object

```

  asyncData() {
     return {
       // this property will get merged into the data object 
       stuff: 'stuff',
     }

   },

   ```
* asyncData runs on the server side - no access  to the window object or window methods like fetch used previously
* Can remove data() object entirely when using `asyncData` as it makes it redundant
* API works as before but this time the data is pre-rendered: meaning it runs on the server before the page is served. Benefit of this is that when a crawler tries to crawl page, all data will be there. Can check this by refreshing page & seeing no http request to browser. Only happens on the initial request.
* `asyncData` runs before the component is initialized => we don't have access to the component's instance as `this`
* This is where the nuxt `context` object is very useful as it contains a lot of helpful information
* Context contains info re: currentRoute for intsance e.g.  base: '/' - can even get the params out of this
* Ajax call takes place on the server side on the initial run - so the user will never face an empty page & get SEO benefits (i.e. crawlers always finding data)
* This means head method can work with params etc when using asyncData whereas previously this wasn't possible
* Nuxt waits for asyncData to complete before running rest methods - this sets meta tags properly