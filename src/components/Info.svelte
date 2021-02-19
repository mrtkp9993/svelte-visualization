<script>
    import Alert from 'svelte-materialify/src/components/Alert';
    export let msg;
</script>

<Alert class="primary-color">
    {msg}
</Alert>