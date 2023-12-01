<script>
    export let flightInfo = [];

</script>

<main>
    {#each flightInfo as flight }
        <div>
            <span> {flight.flightNumber}</span>
            <span> {flight.price}</span>
            <span> {flight.departureDate}</span>
            <span> {flight.departureTime}</span>
        </div>
    {/each}
</main>