<script>
  import { creditStore, gradeStore } from "../store/store";
  import Input from "../lib/Input.svelte";
  let arr = [1, 1, 1, 1, 1, 1];

  let gradeArr = [];
  let creditArr = [];

  $: gradeArr = Object.values($gradeStore).filter(
    (value) => !Number.isNaN(value)
  );
  $: creditArr = Object.values($creditStore).filter(
    (value) => value !== undefined && !Number.isNaN(value)
  );

  let gpa;

  $: gsum = gradeArr.reduce(
    (accumulator, currentValue) => accumulator + currentValue,
    0
  );
  $: csum = creditArr.reduce(
    (accumulator, currentValue) => accumulator + currentValue,
    0
  );

  $: gpa = (gsum / csum).toFixed(2);
</script>

<svelte:head>
  <title>SRM GPA Calculator | SRM Institute of Science and Technology</title>
</svelte:head>
<div class=" flex justify-center mt-10 mb-8">
  <h2 class=" text-xl md:text-3xl text-blue-500 font-bold">
    SRM University <span class=" text-white font-normal">GPA Calculator</span>
  </h2>
</div>
<div class=" flex justify-center">
  <div>
    <table class=" text-white">
      <tr
        ><th> Course </th>
        <th> Credits </th>
        <th> Grade </th></tr
      >
      {#each arr as _, i}
        <Input {i} />
      {/each}
    </table>
    <div class="text-center text-white mt-4">
      <button
        on:click={() => {
          arr = [...arr, 1];
        }}
        class=" border-[1px] border-white h-9 px-2 rounded-md mx-1 hover:bg-gray-100 hover:text-black active:bg-gray-300"
        >Add Course</button
      >
      <button
        on:click={() => {
          location.reload();
        }}
        class=" border-[1px] border-red-600 h-9 px-2 rounded-md mx-1 hover:bg-red-500 active:bg-red-700"
        >Reset</button
      >
    </div>
  </div>
</div>

{#if !Number.isNaN(parseInt(gpa))}
  <div class=" text-white text-center my-10">
    <h1 class="m-3 font-semibold inline">
      Your GPA <span class=" text-4xl text-blue-500 animate-pulse">{gpa}</span>
    </h1>
  </div>
{/if}
