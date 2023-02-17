## 1. Accessing Data
```js
let data = []
 d3.csv(
   "https://raw.githubusercontent.com/barnarderc/workshops/master/pokemon.csv"
 ).then(res => {
   data = res.slice(0, 200);
 });
```

## 2. Plotting Circles
```js
{#each data as d}
<circle cx="10" cy="10" r="5" fill="teal"></circle>
{/each}
```

## 3. Accessing X and Y values
```
const xAccess = d => parseFloat(d.weight_kg)
const yAccess = d => parseInt(d.sp_attack)
```

## 4. Creating Width and Height Variables
```
let width = 500
let height = 500
```

## 5. Creating Scales
```
 $: xScale = d3.scaleLinear()
   .domain(d3.extent(data, xAccess))
   .range([0, width])
	.nice(true)
 $: yScale = d3.scaleLinear()
   .domain(d3.extent(data, yAccess))
   .range([0, height])
```

## 6. Creating Bounds 
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

## 7. Shifting our Data
```
<g transform="translate({margin.left}, {margin.top})">
```

## 8. Shift to a different example to look at a line chart
```
 $: lineGenerator = d3.line()
 .x(d=> xScale(xAccess(d)))
 .y(d=>yScale(yAccess(d)))
 $: lineData = lineGenerator(data)
```

## 9. Make the path 
```
<path d={lineData} fill="none" stroke="sienna">
     </path>
```

## 10. Import Axis Components
```
import AxisX from "./AxisX.svelte";
import AxisY from "./AxisY.svelte";
```

## 11. Update Line
```
x1={scale.range()[1]}
```

## 12. Calculate Tick Points
```
export let count;
$: ticks = scale.ticks(count);
```

## 13. Use a g element to move our ticks 
```
<g transform="translate({scale(x)}, 0)">
```

## 14. Add tick marks 
```
<line
    y1="0"
    y2="10"
    stroke="black"
/>
```

## 15. Add Text for Ticks 
```
<text y="15"
    text-anchor="middle"
    dominant-baseline="hanging">
    {x}
</text>
```

## 16. Axis Label
```
<text x={scale.range()[1]} y="-9" text-anchor="end">
{varName}
</text>
```

## 17. Figure element to make our chart responsive 
```
<figure class="wrapper" 
    bind:clientWidth={width}
    bind:clientHeight={height}>
```

## 18. Wrapper Styling 
```
.wrapper {
   margin: 0;
   font-family: sans-serif;
   width: 100%;
   height: 300px;
   min-width: 0;
 }
```

## 19. Title Styling
```
h2 {
   text-align: center;
   font-family: sans-serif;
   font-size: 2rem;
 }
```

## 20. Interactivity 
```
on:mouseover={() => hoveredData = d}
```

## 21. Tooltip 
```
 {#if hoveredData}
      <Tooltip 
         x={xScale(xAccess(hoveredData))} 
         y={yScale(yAccess(hoveredData))}
         data={hoveredData} />
 {/if}
```

## 22. Create Tooltip File
```
<script>
 export let data;
 export let x;
 export let y;

 let tooltipWidth = 50;
</script>

<div
 class="tooltip"
 style="position: absolute; top: {y + 20}px; left: {x+20}px"
{width}>
 <h3>{data.name} {data.sp_attack}</h3>
 <h4>{data.weight_kg} kg</h4>
</div>
```

## 23. Tooltip Styling
```
 .tooltip {
   padding: 8px 6px;
   background: white;
   box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
   border-radius: 3px;
   pointer-events: none;
 }
```

## 24. Remaining Styling 
```
h3,
 h4 {
   margin: 0;
   padding: 0;
   font-weight: 300;
 }


 h3 {
   font-size: 1rem;
   font-weight: 400;
   margin-bottom: 6px;
   width: 100%;
 }


 h4 {
   font-size: 0.8rem;
   text-transform: uppercase;
 }

 span {
   background: #dda0dd50;
   font-size: 80%;
   margin-left: 2px;
   padding: 2px 4px;
   display: inline-block;
   vertical-align: bottom;
   border-radius: 3px;
   color: rgba(0, 0, 0, 0.7);
 }
```

## 25. Importing a Transition
```
import { fly } from "svelte/transition";
```

## 26. Applying the Transition to the Tooltip
```
transition:fly={{ y: 10 }}
```

## 27. Transition to our Circles
```
transition:fly={{ x: 30, y: 30, delay: 10*i}}
```

## 28. Adjust Styling for Hovered Point
```
r={hoveredData ===d? 10:5 }
       fill={hoveredData ===d? "cyan":"teal" }
       stroke={hoveredData ===d? "white":"teal" }
       stroke-width={hoveredData ===d? 3:0 }
```

## 29. Removing tooltip and Accessibility
```
on:mouseleave={() => hoveredData = null}
on:focus={() => hoveredData = d}
tabindex="0"
```

## 30. Adding Label 
```
 <path d="M 410 20 S 430 20 430 10" fill="none" stroke="red"> </path>
 <text x="260" y="20"
    dominant-baseline="middle"
    font-size="10px"
    >Diancie has the max base attack</text>
   </g>
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
