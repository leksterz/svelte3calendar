<script>
  import DatePicker from "./DatePicker.svelte";

  // has current date
  let currentDate = new Date();

  //
  const onDateChange = (d) => {
    currentDate = d.detail;
  };

  // availability objects
  let schedule = [
    {
      121: true,
      12: true,
      23: true,
    },
    {
      121: false,
      12: false,
      23: true,
    },
  ];
</script>

<h1>Explode Booking</h1>
<p>See availability below</p>
<!-- 
DatePicker component
Upstream Event - on:datechange (executes onDateChange)
Param 1 - currentDate param (based on current date)
-->
<DatePicker
  on:datechange={onDateChange}
  selected={currentDate}
  isAllowed={(date) => {
    const millisecs = date.getTime();
    if (millisecs + 25 * 3600 * 1000 < Date.now()) return false;
    if (millisecs > Date.now() + 3600 * 24 * 10 * 1000) return false;
    return true;
  }} />

{#each schedule as day}
  <p>{day[121]}</p>
  <p>{day[12]}</p>
  <p>{day[23]}</p>
{/each}

<!--
  // setInterval(() => {
  //   currentDate = new Date(currentDate.getTime() + 24 * 3600 * 1000);
  // }, 1000);

  // const isAllowed = date => {
  //   const millisecs = date.getTime();
  //   if (millisecs + 25 * 3600 * 1000 < Date.now()) return false;
  //   if (millisecs > Date.now() + 3600 * 24 * 30 * 1000) return false;
  //   return true;
  // };
-->
