<script>

    import Button from "sveltestrap/src/Button.svelte";
    import { pop } from "svelte-spa-router";

    const URL_BASE = "api/v1/mercados";

    async function loadGraph() {

        const resData = await fetch(URL_BASE);
        let MyData = await resData.json();

        let regions = Array.from(MyData.map((d) => { return d.Region + " " + d.Country; }));
        let population = Array.from(MyData.map((d) => { return parseFloat(d.Population); }));
        let internet_pop = Array.from(MyData.map((d) => { return parseFloat(d.Internet_pop); }));
        console.log("Población:");
        console.log(population);
        console.log("Usuarios:");
        console.log(internet_pop);

        console.log("Grafico 1");

        Highcharts.chart('container', {
            chart: {
                type: 'bar'
            },
            title: {
                text: 'Mercados por región.'
            },
            subtitle: {
                text: 'Fuente: <a href="https://newzoo.com/insights/rankings/top-10-countries-by-game-revenues/"></a>'
            },
            xAxis: {
                categories: regions,
                title: {
                    text: null
                }
            },
            plotOptions: {
                bar: {
                    dataLabels: {
                        enabled: true
                    }
                }
            },
            legend: {
                layout: 'vertical',
                align: 'right',
                verticalAlign: 'top',   
                floating: true,
                borderWidth: 1,
                backgroundColor:
                    Highcharts.defaultOptions.legend.backgroundColor || '#FFFFFF',
                shadow: true
            },
            credits: {
                enabled: false
            },
            series: [{
                name: 'Poblacion (personas)',
                data: population
            }, {
                name: 'Usuarios (personas)',
                data: internet_pop
            }]
        });
    }

</script>

<svelte:head>
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/modules/series-label.js"></script>
    <script src="https://code.highcharts.com/modules/exporting.js"></script>
    <script src="https://code.highcharts.com/modules/export-data.js"></script>
    <script src="https://code.highcharts.com/modules/accessibility.js" on:load="{loadGraph}" defer></script>
</svelte:head>

<main>
    <h2>Gráfico 1 de mercados de juegos por región</h2>
    <p></p>
    <button type="button"  onclick="window.location.href='#/'"> ATRAS</button>
    <figure class="highcharts-figure">
        <div id="container"></div>
        <p style= "font-weight: bold;" class="highcharts-description">
            Esta tabla presenta los 10 principales mercados de juegos clasificados según la poblacion y usuarios que tiene cada región y pais para 2020.
        </p>
        <p></p>
        <button type="button"  onclick="window.location.href='#/'"> ATRAS</button>
    </figure>
    
</main>

<style>
    .highcharts-figure, .highcharts-data-table table {
        min-width: 310px; 
        max-width: 1000px;
        margin: 1em auto;
    }
    
    #container {
        height: 1000px;
    }
    
    .highcharts-data-table table {
        font-family: Verdana, sans-serif;
        border-collapse: collapse;
        border: 1px solid #EBEBEB;
        margin: 10px auto;
        text-align: center;
        width: 100%;
        max-width: 500px;
    }
    .highcharts-data-table caption {
        padding: 1em 0;
        font-size: 1.2em;
        color: #555;
    }
    .highcharts-data-table th {
        font-weight: 600;
        padding: 0.5em;
    }
    .highcharts-data-table td, .highcharts-data-table th, .highcharts-data-table caption {
        padding: 0.5em;
    }
    .highcharts-data-table thead tr, .highcharts-data-table tr:nth-child(even) {
        background: #f8f8f8;
    }
    .highcharts-data-table tr:hover {
        background: #f1f7ff;
    }

    main{
        text-align:center;
        font-weight: bold;
    }

    a.button {
    -webkit-appearance: button;
    -moz-appearance: button;
    appearance: button;
    font-weight: bold;
    text-decoration: none;
    color: initial;
}
    </style>
    