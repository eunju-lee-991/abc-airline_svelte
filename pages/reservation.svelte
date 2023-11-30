<script>
    import axios from "axios";
    import { onMount } from "svelte";
    import Airport from "../components/reservation/airport.svelte";
    import Flatpickr from "svelte-flatpickr";
    import "flatpickr/dist/flatpickr.css";

    let showDepartures = false;
    let showArrivals = false;
    let departureInfos = [];
    let arrivalInfos = [];
    let selecteDeparture = "";
    let selecteArrival = "";
    let selectedDate;

    const handleDepartureSelection = (selected) => {
        console.log("Departure " + selected.detail);
        selecteDeparture = selected.detail;
        showDepartures = false;
    };

    const handleArrivalSelection = (selected) => {
        console.log("Arrival " + selected.detail);
        selecteArrival = selected.detail;
        showArrivals = false;
    };

    const getDepartures = () => {
        showDepartures = !showDepartures;
        if (showDepartures) {
            axios
                .get("http://localhost:8080/api/flights/departures")
                .then((response) => {
                    console.log(response.data.count);
                    console.log(response.data.data);
                    departureInfos = response.data.data;
                })
                .catch((error) => {
                    console.log(error.response);
                });
        }
    };

    const getArrivals = () => {
        showArrivals = !showArrivals;
        if (showArrivals) {
            axios
                .get("http://localhost:8080/api/flights/arrivals")
                .then((response) => {
                    console.log(response.count);
                    console.log(response.data);
                    arrivalInfos = response.data.data;
                })
                .catch((error) => {
                    console.log(error.response);
                });
        }
    };

    const findFlights = () => {
        console.log("selectedDate " + selectedDate);
        axios
            .get("http://localhost:8080/api/flights", {
                params: {
                    departure: selecteDeparture,
                    arrival: selecteArrival,
                    date: selectedDate,
                },
            })
            .then((response) => {
                console.log(response);
            })
            .catch((error) => {
                console.log(error.response);
            });
        selectedDate;
    };

    const options = {
        enableTime: false,
        dateFormat: "Y-m-d",
    };
</script>

<main>
    <div>
        <div class="ticketing-target">
            <div>
                <button
                    type="button"
                    class="departure-select"
                    on:click={getDepartures}
                >
                    <span>출발지</span>
                </button>
                <input type="hidden" id="departureCode" />
                <h2>{selecteDeparture}</h2>
                {#if showDepartures}
                    <Airport
                        airportInfos={departureInfos}
                        on:selection={handleDepartureSelection}
                    />
                {/if}
            </div>

            <div>
                <button
                    type="button"
                    class="arrival-select"
                    on:click={getArrivals}
                >
                    <span>도착지</span>
                </button>
                <input type="hidden" id="ArrivalCode" />
                <h2>{selecteArrival}</h2>
                {#if showArrivals}
                    <Airport
                        airportInfos={arrivalInfos}
                        on:selection={handleArrivalSelection}
                    />
                {/if}
            </div>
        </div>

        <div class="date-select">
            <Flatpickr bind:value={selectedDate} {options} />
        </div>
    </div>
    <button type="button" class="search" on:click={findFlights}> 검색 </button>
</main>

<style>
    .ticketing-target {
        display: flex;
        justify-content: center;
        gap: 100px; /* 원하는 간격 크기로 조정 */
    }

    button {
        background-color: rgb(248, 243, 243); /* 네비게이션바 배경색 */
        color: rgb(12, 12, 12); /* 텍스트 색상 */
        font-size: 28px;
        padding: 10px; /* 내부 여백 */
        margin: 20px 0; /* 위아래 마진 (간격) */
        border: 3px solid #808080; /* 자연스러운 회색 테두리 설정 */
        text-align: center; /* 텍스트 정렬 */
        text-decoration: none; /* 밑줄 제거 */
        display: inline-block;
        cursor: pointer; /* 마우스 커서 포인터로 변경 */
        width: 150px; /* 버튼이 100%의 너비를 차지하도록 설정 */
        box-sizing: border-box; /* 여백과 테두리를 포함한 전체 박스 크기로 설정 */
    }

    .search {
        background-color: rgb(61, 61, 61); /* 네비게이션바 배경색 */
        color: rgb(247, 243, 243); /* 텍스트 색상 */
        font-size: 20px;
        padding: 5px; /* 내부 여백 */
        margin: 100px 0; /* 위아래 마진 (간격) */
        border: none; /* 자연스러운 회색 테두리 설정 */
        text-align: center; /* 텍스트 정렬 */
        text-decoration: none; /* 밑줄 제거 */
        display: inline-block;
        cursor: pointer; /* 마우스 커서 포인터로 변경 */
        width: 120px;
        box-sizing: border-box; /* 여백과 테두리를 포함한 전체 박스 크기로 설정 */
    }
</style>
