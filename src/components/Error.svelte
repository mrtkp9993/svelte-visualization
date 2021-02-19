<script>
    import Alert from 'svelte-materialify/src/components/Alert';
    export let msg;
</script>

<Alert class="error-color">
    {msg}
</Alert>