# starbase-router

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).


### Notes
Two way to solve `Prop being mutated: "result" `
we cannot change props by child components
* First solution
```js
data () {
  anotherNameforProp1: Prop1
}
```
```js
// Replace all the {{Prop1}} by {{anotherName}} 
this.item = blabla
// change to
this.anotherName = blabla
```

* Second solution
```js
// Child <script>
props: ['item']
// change to
props: ['passedItem']

// and 

data() {
  return {
    item: {}
  }
}, 
created() {
  this.item = this.passedItem
}
```
```html
// Parent template
<Child :item="item">
  /* change to */
<Child :passed-item="item">

```