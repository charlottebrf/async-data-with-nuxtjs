# Axios

* Compatible with the browser & Node environment - this is why it's a good fit for Nuxt apps
* Can still use it when running code on Server Side


# Axios module
* Nuxt Axios Module => modules are functions called sequentially when booting Nuxt.
* Nuxt waits for each module to finish before continuing
* Because of this, modules can customise every aspect of Nuxt
* Axios module makes Axios globally available in application - no need to import in each file
* Can set a baseUrl which will be set in both client & server side - can use Proxy Module
* Can use `$axios` - extracted out from the context. Using `$axios`  & `$get` instead of return response object - get the data back directly
* Can use `$axios.get` to get just object back 
