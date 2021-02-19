<script>
    import { Datatable, rows } from 'svelte-simple-datatables'

    const settings = {
        sortable: false,
        pagination: true,
        rowPerPage: 50,
        columnFilter: true,
    }

    export let data;
</script>

    <Datatable settings={settings} data={data}>
        <thead>
        <th data-key="time">Time</th>
        <th data-key="title">Title</th>
        <th data-key="mag">Magnitude</th>
        <th data-key="place">Place</th>
        </thead>
        <tbody>
        {#each $rows as row}
            <tr>
                <td>{row.properties.time}</td>
                <td>{row.properties.title}</td>
                <td>{row.properties.mag}</td>
                <td>{row.properties.place}</td>
            </tr>
        {/each}
        </tbody>
    </Datatable>
