<script lang="ts">
  let counter = 0;
  //The $: means re run this if any of the referenced value changed
  //A useEffect that is maybe not cringe
  $: doubled = counter * 2;
  $: {
    console.log("The value of count is: ", counter);
    console.log("The value of doubled count is: ", doubled);
  }
  $: if (counter === 10) {
    alert("The counter is now at 10");
  }

  function incrementCounter() {
    counter += 1;
  }

  let numbers = [1, 2, 3, 4];
  $: sum = numbers.reduce((a, b) => a + b, 0);

  function addNumber() {
    //Reactivity is achieved by directly assigning the variable directly
    //This works
    numbers = [...numbers, numbers.length + 1];

    //This also works
    //numbers.push(numbers.length + 1);
    //numbers = numbers;

    //Or this
    //numbers[numbers.length] = numbers.length + 1;

    //This would not
    //numbers.push(numbers.length + 1);

    //this also wont, because it was not assigned to numbers directly
    //const temp = numbers
    //temp[numbers.length] = numbers.length + 1;
  }
</script>

<button on:click={incrementCounter}>
  <!--Svelte keeps the value of the dom and this variable in sync-->
  Clicked {counter} {counter === 1 ? "time" : "times"}
</button>
<!--Alternatively {count * 2} would also work-->
<p>The doubled count is {doubled}</p>
<p>{numbers.join(" + ")} = {sum}</p>
<button on:click={addNumber}>Add next number</button>