# Links We'll Be Working with Today: 

The links will also be relinked below where they get used. 
1. [Code Sandbox](https://codesandbox.io/dashboard)
2. [SVG Starter](https://codesandbox.io/s/svg-starter-mv89zw)
3. [Visualization Starter Code](https://codesandbox.io/s/october-workshop-data-viz-starter-ct37tm?file=/App.svelte)
4. [Final Visualization](https://codesandbox.io/s/in-progress-pokemon-kq4v56?file=/App.svelte)
5. [Slides](https://docs.google.com/presentation/d/1sxygSHBJEcQXmhciRbjDDz87WXcWXBIHlPDl0CU_Taw/edit?usp=sharing)
6. [W3 Schools CSS](https://www.w3schools.com/css/css_intro.asp)

# SVGs/Svelte Intro

## Open this Sandbox on Code Sandbox:
[SVG Starter Code Sandbox](https://codesandbox.io/s/svg-starter-mv89zw)

# Making Our Data Viz in Svelte

## Open the sandbox link below and fork it to copy and make your own.  
[Sandbox Example](https://codesandbox.io/s/october-workshop-data-viz-starter-ct37tm?file=/App.svelte)

## This is what we are working towards. 
[Final Visualization](https://codesandbox.io/s/in-progress-pokemon-kq4v56?file=/App.svelte)

## 1. Creating Scales
```js
 $: xScale = d3.scaleLinear()
   .domain(d3.extent(data, xAccess))
   .range([0, width])
	.nice(true)
 $: yScale = d3.scaleLinear()
   .domain(d3.extent(data, yAccess))
   .range([0, height])
```

## 2. Creating Bounds 
```js
 let boundsWidth = width - margin.left - margin.right
 let boundsHeight = height - margin.top - margin.bottom
```

## 3. Shifting our Data
```js
<g transform="translate({margin.left}, {margin.top})">
```

## 4. Import Axis Components
```js
import AxisX from "./AxisX.svelte";
import AxisY from "./AxisYOriginal.svelte";
```

## 5. Move Our X Axis Over
```js
<g transform="translate({margin.left}, {boundsHeight + margin.top})">
```

## 6. Figure element to make our chart responsive 
```js
<figure class="wrapper" 
    bind:clientWidth={width}
    bind:clientHeight={height}>
```

## 7. Interactivity 
```js
on:mouseover={() => hoveredData = d}
```

## 8. Adjust Styling for Hovered Point
```js
r={hoveredData ===d? 10:5 }
fill={hoveredData ===d? "cyan":"teal" }
stroke={hoveredData ===d? "white":"teal" }
stroke-width={hoveredData ===d? 3:0 }
```

## 9. Removing Hover and Adding Accessibility
```js
on:mouseleave={() => hoveredData = null}
on:focus={() => hoveredData = d}
tabindex="0"
```

## 10. Update Line
```js
x1={scale.range()[1]}
```

## 11. Calculate Tick Points
```js
export let count;
$: ticks = scale.ticks(count);
```

## 12. Use a g element to move our ticks 
```js
<g transform="translate({scale(x)}, 0)">
```

## 13. Add tick marks 
```js
<line
    y1="0"
    y2="10"
    stroke="lightgray"
/>
```

## 14. Add Text for Ticks 
```js
<text y="15"
    text-anchor="middle"
    dominant-baseline="hanging">
    {x}
</text>
```

## 15. Axis Label
```js
<text x={scale.range()[1]} y="-9" text-anchor="end">
{varName}
</text>
```

## 16. Tooltip 
```js
 {#if hoveredData}
      <Tooltip 
         x={xScale(xAccess(hoveredData))} 
         y={yScale(yAccess(hoveredData))}
         data={hoveredData} />
 {/if}
```

## 17. Create Tooltip File
```js
<script>
 export let data;
 export let x;
 export let y;

 let tooltipWidth = 50;
</script>

<div
 class="tooltip"
 style="position: absolute; top: {y + 20}px; left: {x+20}px"
{tooltipWidth}>
 <h3>{data.name} {data.sp_attack}</h3>
 <h4>{data.weight_kg} kg</h4>
</div>
```

## 18. Tooltip Styling
```js
 .tooltip {
   padding: 8px 6px;
   background: white;
   box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
   border-radius: 3px;
   pointer-events: none;
 }
```

## 19. Remaining Styling 
```js
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

## 20. Importing a Transition
```js
import { fly } from "svelte/transition";
```

## 21. Applying the Transition to the Tooltip
```js
transition:fly={{ y: 10 }}
```

## 22. Transition to our Circles
```js
transition:fly={{ x: 30, y: 30, delay: 10*i}}
```

