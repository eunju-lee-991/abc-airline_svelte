<script>
    export let airportInfos = [];
    import { createEventDispatcher } from "svelte";
    let selected = "Asia";

    const dispatch = createEventDispatcher();

    const selectContinent = (event) => {
        const prevSelectedButton = document.querySelector(
            ".navbar-button.selected",
        );
        if (prevSelectedButton) {
            prevSelectedButton.classList.remove("selected");
        }

        selected = event.target.dataset.value;
        event.target.classList.add("selected");
    };

    const selectAirport = (event) => {
        const selectedAirport = event.target.dataset.value;
        console.log("selectedAirport : " + selectedAirport);
        dispatch('selection', selectedAirport);
    };
</script>

<main>
    <div class="container">
        <div class="left-continent">
            <button
                on:click={selectContinent}
                data-value="Asia"
                class="navbar-button selected">Asia</button
            >
            <button
                on:click={selectContinent}
                data-value="America"
                class="navbar-button">America</button
            >
            <button
                on:click={selectContinent}
                data-value="Europe"
                class="navbar-button">Europe</button
            >
            <button
                on:click={selectContinent}
                data-value="Oceania"
                class="navbar-button">Oceania</button
            >
            <button
                on:click={selectContinent}
                data-value="Africa"
                class="navbar-button">Africa</button
            >
        </div>
        <div class="right-airport">
            <div>
                {#each airportInfos as airport}
                    {#if selected == airport.continent}
                        <button
                            class="airport-info"
                            on:click={selectAirport}
                            data-value={airport.iatacode}
                        >
                            {airport.city} ({airport.iatacode})
                        </button>
                    {/if}
                {/each}
            </div>
        </div>
    </div>
</main>

<style>
    .container {
        display: flex;
        height: 500px;
    }

    .left-continent {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: 200px;
    }

    .right-airport {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-left: 20px;
        margin-top: 20px;
        width: 200px;
    }
    .airport-info {
        margin-bottom: 0px;
        background-color: rgb(204, 207, 204); /* 네비게이션바 배경색 */
        color: rgb(5, 5, 5); /* 텍스트 색상 */
        padding: 10px; /* 내부 여백 */
        margin: 0 0; /* 위아래 마진 (간격) */
        border: none; /* 테두리 없음 */
        text-align: left; /* 텍스트 정렬 */
        text-decoration: none; /* 밑줄 제거 */
        display: inline-block;
        cursor: pointer; /* 마우스 커서 포인터로 변경 */
        width: 100%; /* 버튼이 100%의 너비를 차지하도록 설정 */
        box-sizing: border-box; /* 여백과 테두리를 포함한 전체 박스 크기로 설정 */
    }
    .navbar-button {
        background-color: #4caf50; /* 네비게이션바 배경색 */
        color: white; /* 텍스트 색상 */
        padding: 10px; /* 내부 여백 */
        margin: 0 0; /* 위아래 마진 (간격) */
        border: none; /* 테두리 없음 */
        text-align: left; /* 텍스트 정렬 */
        text-decoration: none; /* 밑줄 제거 */
        display: inline-block;
        cursor: pointer; /* 마우스 커서 포인터로 변경 */
        width: 100%; /* 버튼이 100%의 너비를 차지하도록 설정 */
        box-sizing: border-box; /* 여백과 테두리를 포함한 전체 박스 크기로 설정 */
    }

    .selected {
        background-color: #023b04; /* 선택된 버튼에 대한 색상 변경 */
    }
</style>
