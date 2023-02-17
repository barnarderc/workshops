# SVGs
## 1. Create SVG
```html
<svg width="500" height="300"  style="border: 1px solid red">
</svg>
```
## 2. Text for Context
```html
<text x="{100-75}" y="10" fill="blue" style="font-size: 12px" dominant-baseline="middle"> X: 100 y:10</text>
<text x="{100-80}" y="160" fill="blue" style="font-size: 12px" dominant-baseline="middle">X: 100 y:160</text>
<text x="{100-80}" y="210" fill="blue" style="font-size: 12px" dominant-baseline="middle">X: 100 y:210</text>
<text x="{400+10}" y="10" fill="blue" style="font-size: 12px" dominant-baseline="middle"> X: 400 y:10</text>
<text x="{400+10}" y="160" fill="blue" style="font-size: 12px" dominant-baseline="middle">X: 400 y:160</text>
<text x="{400+10}" y="210" fill="blue" style="font-size: 12px" dominant-baseline="middle">X: 400 y:210</text>
```

## 3. Rect
```html
<rect x="100" y="10" width="300" height='200' fill="none" stroke="black" stroke-width="10" rx="20"> </rect>
<rect x="100" y="160"width="300" height='50' fill="black" stroke="black" stroke-width="5" rx="10"> </rect>
```

## 4. Circle
```html
<circle cx="250" cy="185" r="10" fill="white"></circle>
```

## 5. Line
```html
<line x1="105" y1="110" x2="150" y2="80" stroke="red" stroke-width="5"> </line>
```

## 6. Polyline
```html
<polyline points="150,80 190,130 280,60 320,100 370, 65" fill="none" stroke="red" stroke-width="5"> </polyline>
```

## 7. Polygon
```html
<polygon points="230,220 270,220 300,270 200,270" fill="black"> </polygon>
```

## 8. Path
```html
<path d="M 260 30 S 280 30 280 50" fill="none" stroke="green"> </path>
```

## 9. Text
```html
<text x="260" y="30" 
dominant-baseline="middle"
text-anchor="end
font-size="10px"
>Some text here</text>
```

# Making Our Data Viz in Svelte

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
```js
const xAccess = d => parseFloat(d.weight_kg)
const yAccess = d => parseInt(d.sp_attack)
```

## 4. Creating Width and Height Variables
```js
let width = 500
let height = 500
```

## 5. Creating Scales
```js
 $: xScale = d3.scaleLinear()
   .domain(d3.extent(data, xAccess))
   .range([0, width])
	.nice(true)
 $: yScale = d3.scaleLinear()
   .domain(d3.extent(data, yAccess))
   .range([0, height])
```

## 6. Creating Bounds 
```js
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
```js
<g transform="translate({margin.left}, {margin.top})">
```

## 8. Shift to a different example to look at a line chart
```js
 $: lineGenerator = d3.line()
 .x(d=> xScale(xAccess(d)))
 .y(d=>yScale(yAccess(d)))
 $: lineData = lineGenerator(data)
```

## 9. Make the path 
```js
<path d={lineData} fill="none" stroke="sienna">
     </path>
```

## 10. Import Axis Components
```js
import AxisX from "./AxisX.svelte";
import AxisY from "./AxisY.svelte";
```

## 11. Update Line
```js
x1={scale.range()[1]}
```

## 12. Calculate Tick Points
```js
export let count;
$: ticks = scale.ticks(count);
```

## 13. Use a g element to move our ticks 
```js
<g transform="translate({scale(x)}, 0)">
```

## 14. Add tick marks 
```js
<line
    y1="0"
    y2="10"
    stroke="black"
/>
```

## 15. Add Text for Ticks 
```js
<text y="15"
    text-anchor="middle"
    dominant-baseline="hanging">
    {x}
</text>
```

## 16. Axis Label
```js
<text x={scale.range()[1]} y="-9" text-anchor="end">
{varName}
</text>
```

## 17. Figure element to make our chart responsive 
```js
<figure class="wrapper" 
    bind:clientWidth={width}
    bind:clientHeight={height}>
```

## 18. Wrapper Styling 
```js
.wrapper {
   margin: 0;
   font-family: sans-serif;
   width: 100%;
   height: 300px;
   min-width: 0;
 }
```

## 19. Title Styling
```js
h2 {
   text-align: center;
   font-family: sans-serif;
   font-size: 2rem;
 }
```

## 20. Interactivity 
```js
on:mouseover={() => hoveredData = d}
```

## 21. Tooltip 
```js
 {#if hoveredData}
      <Tooltip 
         x={xScale(xAccess(hoveredData))} 
         y={yScale(yAccess(hoveredData))}
         data={hoveredData} />
 {/if}
```

## 22. Create Tooltip File
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
{width}>
 <h3>{data.name} {data.sp_attack}</h3>
 <h4>{data.weight_kg} kg</h4>
</div>
```

## 23. Tooltip Styling
```js
 .tooltip {
   padding: 8px 6px;
   background: white;
   box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
   border-radius: 3px;
   pointer-events: none;
 }
```

## 24. Remaining Styling 
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

## 25. Importing a Transition
```js
import { fly } from "svelte/transition";
```

## 26. Applying the Transition to the Tooltip
```js
transition:fly={{ y: 10 }}
```

## 27. Transition to our Circles
```js
transition:fly={{ x: 30, y: 30, delay: 10*i}}
```

## 28. Adjust Styling for Hovered Point
```js
r={hoveredData ===d? 10:5 }
fill={hoveredData ===d? "cyan":"teal" }
stroke={hoveredData ===d? "white":"teal" }
stroke-width={hoveredData ===d? 3:0 }
```

## 29. Removing tooltip and Accessibility
```js
on:mouseleave={() => hoveredData = null}
on:focus={() => hoveredData = d}
tabindex="0"
```

## 30. Adding Label if we have time
```js
  $: maxYPoint = d3.greatest(data, yAccess)
```

## 31. Label Div and SVG
```html
{#if maxYPoint}
		<div
			class="label"
			style="border: 2px solid blue; transform: translate({margin.left + xScale(xAccess(maxYPoint))}px, {margin.top}px)">
			<div class="label-contents">
				Diancie has the max base attack. 
			</div>
			<svg width="40" height="20" style="border: 2px solid blue">
				<path d="M 0 0 Q 40 0 40 20"
				stroke="currentColor" fill="none" />
			</svg>
		</div>
{/if}
```

## 32. Label Styling to Position it correctly
```css
.label {
		/*
		one important thing is to
		give the wrapper a "position"
		so it acts as a "position context"
		*/
		position: absolute;
		top: 0;
		left: 0;
		max-width: 8em;
		font-size: 0.6em
	}

.label-contents {
		position: absolute;
		transform: translate(-100%, -100%) translate(-23px, -3px);
		width: 8em;
		text-align: right;
		font-size: 0.8em;
		color: orange;
	}

  .label svg {
		position: absolute;
		right: 0;
		bottom: 0;
    color: orange;
	}
```

```
```

```
```

```
```
