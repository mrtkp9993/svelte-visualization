<script>
    import Bar from "svelte-chartjs/src/Bar.svelte"

    // From: https://stackoverflow.com/questions/36266895/simple-histogram-algorithm-in-javascript
    function histogram(data, size) {
        let min = Infinity;
        let max = -Infinity;

        for (const item of data) {
            if (item < min) min = item;
            else if (item > max) max = item;
        }

        const bins = Math.ceil((max - min + 1) / size);

        const histogram = new Array(bins).fill(0);

        for (const item of data) {
            histogram[Math.floor((item - min) / size)]++;
        }

        return histogram;
    }

    function hist_labels(hist) {
        // 5 is hardcoded, min size of earthquakes
        // 0.2 is histogram bin width
        let labels = Array(hist.length).fill().map((e, i) => 5 + i * 0.2);
        return labels
    }

    export let data;
</script>

<div class="container">
    <Bar data={{labels: hist_labels((histogram(data.map(x => x.properties.mag), 0.2))),
        datasets: [
            {label:'Num of earthquakes',
            data: (histogram(data.map(x => x.properties.mag), 0.2))}
        ]
    }}/>
</div>