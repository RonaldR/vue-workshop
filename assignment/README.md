# Giphy Vue assignment  

## Use the Giphy api to search and show your favorite gifs :)  

- Start new project with Vue CLI
    - `npm install -g @vue/cli`
    - `vue create vue-workshop`
- First build the complete app in 'App.vue'
    - Search form, suggestion buttons, image results
    - You can use styling.css
    - Use Axios or Fetch or whatever to do the api call
- Got this? Awesome! Split the 'App.vue' in components
    - Search form, Suggestion buttons, Image, ??


## Giphy api
https://developers.giphy.com/docs/  

Key:  
cEDADbeB31OKJkua38c8r8BmaFuiHkph  

Full url:  
https://api.giphy.com/v1/gifs/search?api_key=cEDADbeB31OKJkua38c8r8BmaFuiHkph&q=${query}&limit=18&offset=0&rating=R&lang=en

## Vue Docs
https://vuejs.org/v2/guide/

## More time: Event/State management
- Use eventbus: https://alligator.io/vuejs/global-event-bus/
- Or Vuex: https://github.com/vuejs/vuex