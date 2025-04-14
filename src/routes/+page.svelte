
<script>
	import { onMount } from "svelte";
    import { getPressure, start, requestAndStart } from "pressurize-js";
	import Navbar from "./Navbar.svelte";
    
    let elementValues = $state({});


    elementValues.boxDemoPressure = 0;
    elementValues.barDemoPressure = 0;
    function dumbPressureTest() {
        let pressure = 0;
        let intervalId;
        let cnt = 0;
        intervalId = setInterval(() => {
            pressure += getPressure() / (500/20);
            cnt += 1;
            if (cnt > 500/20) {
                clearInterval(intervalId);
            }
            elementValues.boxDemoPressure = pressure;
        }, 20);
    }
</script>
<Navbar></Navbar>
<div class="mainContainer">
    <div class="section header">
        <div>
            <h1>pressurize.js</h1>
            <span>
                The First Open-Source JavaScript Pressure Detection Library for All Mobile Devices Without Specialized Hardware :D
            </span>
        </div>
    </div>
    <div class="section examples" id="examples">
        <h2>Examples :D</h2>
        <button onclick={() => {
            window.location.href = "#color-demo";
        }}>▽</button>
    </div>
    <div class="section color-demo example" id="color-demo">
        <h2>Color Demo</h2>
        <div class="color-demo-container">
            <span>
                Here the color of the box will change based on the pressure applied to the screen, at the time of impact.
            </span>
            <button class="color-demo-box" id="color-demo-box" style="
            background-color: color-mix(in srgb, red {100* (1 - elementValues.boxDemoPressure)}%, green {100*elementValues.boxDemoPressure}%);
            " onclick={() => {
                requestAndStart();
                setTimeout(() => {
                    elementValues.boxDemoPressure = getPressure();
                }, 75*2);
                // dumbPressureTest();

            }}>Pressure: {elementValues.boxDemoPressure.toFixed(2)}</button>
        </div>
    </div>
    <div class="section bar-demo example">
        <h2>Bar Demo</h2>
        <div class="bar-demo-container">
            <span>
                Here the level of green in box will change based on the pressure applied to the screen, at the time of impact.
            </span>
            <button class="bar-demo-box" id="bar-demo-box" onclick={() => {
                requestAndStart();
                setTimeout(() => {
                    elementValues.barDemoPressure = getPressure();
                }, 75*2);
                // dumbPressureTest();
            }} style="background: linear-gradient(to bottom, red 0%, red {100* (1 - elementValues.barDemoPressure)}%, green {100* (1 - elementValues.barDemoPressure)}%, green 100%);">Pressure: {elementValues.barDemoPressure.toFixed(2)}
            </button>
        </div>
    </div>
</div>
<style>
    /* @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap'); */
    * {
        font-family: sans-serif;
        color: var(--platinum);
    }
    :global(body, html) {
        display: flex;
        align-items: center;
        height: 100%;
        width: 100%;
        background-color: white;
        margin: 0px;
        padding: 0px;
        flex-direction: column;
        overflow-x: hidden;
        scroll-behavior: smooth;
    }

    :root {
        /* CSS HEX */
        --burnt-sienna: #dd6e42ff;
        --dutch-white: #e8dab2ff;
        --paynes-gray: #4f6d7aff;
        --columbia-blue: #c0d6dfff;
        --platinum: #eaeaeaff;
    }

    .mainContainer {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        width: 100%;
        height: 100%;
        margin: 0px;
        padding: 0px;
    }
    .section {
        width: 100%;
        margin: 0px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        padding: 2em;
        background-color: var(--burnt-sienna);
        box-shadow: inset 0px 0px 10px 1px rgba(0, 0, 0, 0.2);
        text-align: center;
        font-size: 1.15rem;
        div {
            width: 70%;
        }

        text-shadow: 0px 0px 10px rgba(0, 0, 0, 0.25);
    }

    .header {
        background-color: var(--burnt-sienna);
        font-size: 1.25rem;
        /* box-shadow: 0px 5px 10px 1px rgba(0, 0, 0, 0.2); */
    }

    .examples {
        background-color: var(--columbia-blue);
        font-size: 1.5rem;
        padding: 2em;
        padding-top: 20vh;
        padding-bottom: 3em;
        h2 {
            margin: 0px;
            padding: 0px;
            color: var(--paynes-gray);
        }

        button {
            border: none;
            background-color: transparent;
            font-size: 2rem;
            padding: 0px;
            cursor: pointer;
            margin: 0px;
            color: var(--paynes-gray);
            margin-top: 1em;
        }
    }
    
    .example {
        padding-top: 3em;
        padding-bottom: 3em;
        border-top: var(--paynes-gray) 0.125em solid;
        text-shadow: 0px 0px 10px rgba(0, 0, 0, 0.0625);
    }

    .color-demo {
        background-color: var(--dutch-white);
        font-size: 1.5rem;
        h2 {
            margin: 0px;
            padding: 0px;
            color: var(--paynes-gray);
        }
        .color-demo-container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            .color-demo-box {
                width: 17.5em;
                height: 17.5em;
                background-color: var(--paynes-gray);
                margin: 1em;
                border: 0px;
                box-shadow: inset 0px 0px 10px 1px rgba(0, 0, 0, 0.5);
            }
            span {
                color: color-mix(in hsl, var(--columbia-blue) 25%, var(--paynes-gray) 75%);
            }
        }
    }

    .bar-demo {
        background-color: var(--dutch-white);
        font-size: 1.5rem;
        padding: 1em;
        h2 {
            margin: 0px;
            padding: 0px;
            color: var(--paynes-gray);
        }
        .bar-demo-container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            .bar-demo-box {
                width: 10em;
                height: 17.5em;
                background: linear-gradient(to bottom, red 0%, red 100%, green 100%, green 100%);
                margin: 1em;
                border: 0px;
                box-shadow: inset 0px 0px 10px 1px rgba(0, 0, 0, 0.5);
            }
            span {
                color: color-mix(in hsl, var(--columbia-blue) 25%, var(--paynes-gray) 75%);
            }
        }
    }
</style>
