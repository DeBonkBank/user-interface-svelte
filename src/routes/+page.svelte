<script>
    import { onMount } from 'svelte';
    let rfidMessage = 'Waiting for tag...';

    onMount(() => {
        const socket = new WebSocket('ws://localhost:9000');

        socket.addEventListener('message', (event) => {
            const data = event.data;
            rfidMessage = data;
        });

        socket.addEventListener('open', () => {
            console.log('Connected to WebSocket server');
        });

        socket.addEventListener('error', (err) => {
            console.error('WebSocket error:', err);
        });
    });
</script>

<h1>RFID Reader</h1>
<p>{rfidMessage}</p>
