1. Global Variable

let values = [];

    This is an array to hold the numeric values representing the heights of the bars.

    It is declared globally because multiple functions (generateBars and bubbleSort) need to access and modify it.

2. Function: generateBars

function generateBars() {
  const container = document.getElementById('bar-container');
  container.innerHTML = '';
  values = Array.from({ length: 50 }, () => Math.floor(Math.random() * 100) + 1);

  values.forEach((val) => {
    const bar = document.createElement('div');
    bar.classList.add('bar');
    bar.style.height = `${val * 2}px`;
    container.appendChild(bar);
  });
}

What it does:

    This function creates 50 random values between 1 and 100 and renders them as vertical bars inside a container with the ID bar-container.

Step-by-step:

    const container = document.getElementById('bar-container');

        It selects the HTML element where the bars will be placed.

    container.innerHTML = '';

        Clears any existing bars inside the container to reset the visualization.

    values = Array.from({ length: 50 }, () => Math.floor(Math.random() * 100) + 1);

        Creates an array of length 50 filled with random integers between 1 and 100.

        Array.from is used with a mapping function that generates each random number.

    Then it loops through values with forEach:

        For each val, it creates a new <div> element (the bar).

        Adds a CSS class bar for styling.

        Sets the height of the bar based on the value, multiplied by 2 to make it visually noticeable (val * 2 pixels).

        Appends the bar into the container.

3. Function: bubbleSort

async function bubbleSort() {
  const bars = document.querySelectorAll('.bar');
  for (let i = 0; i < values.length - 1; i++) {
    for (let j = 0; j < values.length - i - 1; j++) {
      bars[j].classList.add('active');
      bars[j + 1].classList.add('active');

      if (values[j] > values[j + 1]) {
        [values[j], values[j + 1]] = [values[j + 1], values[j]];
        bars[j].style.height = `${values[j] * 2}px`;
        bars[j + 1].style.height = `${values[j + 1] * 2}px`;
      }

      await new Promise((resolve) => setTimeout(resolve, 20));

      bars[j].classList.remove('active');
      bars[j + 1].classList.remove('active');
    }
  }
}

What it does:

    This function performs the Bubble Sort algorithm on the values array, while simultaneously updating the visual bars and adding an animation delay so you can watch the sorting in progress.

Key points:

    async function:
    The function is asynchronous because it uses await with a promise-based delay to create pauses between steps for animation.

    const bars = document.querySelectorAll('.bar');
    Selects all the bar elements in the DOM so their heights and styles can be updated during sorting.

    Two nested for loops implement Bubble Sort:

        Outer loop: for (let i = 0; i < values.length - 1; i++)
        Runs the sorting passes. After each pass, the largest remaining unsorted value "bubbles" to the right.

        Inner loop: for (let j = 0; j < values.length - i - 1; j++)
        Compares adjacent elements and swaps them if they are in the wrong order.

Inside the inner loop:

    bars[j].classList.add('active'); and bars[j + 1].classList.add('active');
    Adds an "active" CSS class to highlight the two bars currently being compared.

    if (values[j] > values[j + 1]) { ... }
    Checks if the left value is greater than the right value.

    If yes, swap the two values in the array:

[values[j], values[j + 1]] = [values[j + 1], values[j]];

Then update the heights of the corresponding bars to reflect the swapped values:

    bars[j].style.height = `${values[j] * 2}px`;
    bars[j + 1].style.height = `${values[j + 1] * 2}px`;

    The await new Promise((resolve) => setTimeout(resolve, 20)); line:

        Creates a 20-millisecond delay before continuing, allowing the browser to visually render the swap and highlight before moving on.

        This is what creates the smooth animation effect.

    After the delay, the "active" class is removed from the compared bars, so the highlight disappears.

4. Event Listeners

document.getElementById('generateBtn').addEventListener('click', generateBars);
document.getElementById('bubbleSortBtn').addEventListener('click', bubbleSort);

    These lines attach event listeners to buttons with IDs generateBtn and bubbleSortBtn.

    When the user clicks the Generate button, a new random set of bars is created.

    When the user clicks the Bubble Sort button, the sorting animation begins.

5. Initial Call

generateBars();

    When the page loads, generateBars() is called to create the initial set of random bars so the user sees something right away.

Summary:

    generateBars: Creates 50 random bars with heights based on random values.

    bubbleSort: Animates the sorting process by repeatedly swapping adjacent bars if out of order, with delays to show each step.

    Event listeners trigger these actions when the user clicks buttons.

    The entire script demonstrates Bubble Sort visually and interactively on a web page.# sorting-visualizer
Visualize sorting algorithms with colorful animated bars!
