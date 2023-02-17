```js
let data = []
 d3.csv(
   "https://raw.githubusercontent.com/barnarderc/workshops/master/pokemon.csv"
 ).then(res => {
   data = res.slice(0, 200);
 });
```

```js
{#each data as d}
<circle cx="10" cy="10" r="5" fill="teal"></circle>
{/each}
```

```
const xAccess = d => parseFloat(d.weight_kg)
const yAccess = d => parseInt(d.sp_attack)
```

```
let width = 500
let height = 500
```

```
 $: xScale = d3.scaleLinear()
   .domain(d3.extent(data, xAccess))
   .range([0, width])
	.nice(true)
 $: yScale = d3.scaleLinear()
   .domain(d3.extent(data, yAccess))
   .range([0, height])
```

```
let margin = {
   left: 30,
   top: 0,
   right: 10,
   bottom: 30
 };

 let boundsWidth = width - margin.left - margin.right
 let boundsHeight = height - margin.top - margin.bottom
```

```
<g transform="translate({margin.left}, {margin.top})">
```

```
import AxisX from "./AxisX.svelte";
import AxisY from "./AxisY.svelte";
```

```
x1={scale.range()[1]}
```

```
export let count;
$: ticks = scale.ticks(count);
```

```
<g transform="translate({scale(x)}, 0)">
```

```
```

```
```

```
```


```
```

```
```

```
```

```
```

```
```


```
```

```
```

```
```

```
```

```
```


```
```

```
```

```
```

```
```

```
```


```
```

```
```

```
```

```
```

```
```
