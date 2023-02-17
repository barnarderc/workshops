```js
 d3.csv(
   "https://raw.githubusercontent.com/barnarderc/workshops/master/pokemon.csv"
 ).then(res => {
   data = res.slice(0, 200);
 });
```
