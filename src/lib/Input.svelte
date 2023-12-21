<script>
  import { creditStore, gradeStore } from "../store/store";

  export const csr = false;
  export let i;

  let red = false;
  let grade;
  let credit;

  let dic = { O: 10, "A+": 9, A: 8, "B+": 7, B: 6, C: 5, F: 0, Ab: 0 };

  $: total = parseInt(credit) * dic[grade];

  $: creditStore.update((a) => {
    return { ...a, [i + 1]: credit };
  });

  $: gradeStore.update((a) => {
    return { ...a, [i + 1]: total };
  });

  const gradeChange = () => {
    red = true;
  };
</script>

<tr>
  <td class=" text-center">{i + 1}</td>
  <input
    type="number"
    name="credit"
    id="credit"
    min="1"
    onkeydown="false"
    bind:value={credit}
    class="bg-[#393E46] m-[0.3rem] rounded-lg pl-2 h-9 border-gray-600 border-0 ring-1 ring-gray-600 outline-none focus:ring-blue-500"
  />

  <td class=" items-center">
    <select
      name="grade"
      id="grade"
      bind:value={grade}
      class=" bg-[#393E46] outline-none rounded-md h-9 ring-1 ring-gray-600 focus:ring-blue-500 {red &
        (grade === '') && 'focus:ring-red-500'}"
      on:change={gradeChange}
    >
      <option value="">Select</option>
      <option value="O">O</option>
      <option value="A+">A+</option>
      <option value="A">A</option>
      <option value="B+">B+</option>
      <option value="B">B</option>
      <option value="C">C</option>
      <option value="F">F</option>
      <option value="Ab">Ab</option>
    </select></td
  >
</tr>
