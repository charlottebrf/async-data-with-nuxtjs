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