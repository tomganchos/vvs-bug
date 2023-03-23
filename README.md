# vvs-bug
Small project to show a vue-virtual-scroller
bug with horizontal scrolling inside item

### install and run
```
npm i

npm run dev
```

### demo
http://kriuchkov.art/vue-virtual-scroller/

### bug
with horizontal scrolling, scrollLeft attribute is added to inner elements of all items, but with vertical scrolling, scrollLeft randomly disappears
