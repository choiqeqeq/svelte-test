<script lang="ts">
  let display = '';

  function handleClick(event: MouseEvent) {
    // 이벤트 핸들러가 보는 MouseEvent가 HTMLInputElement에서 온것임을 알 수 없기에 케스팅 필요함
    // https://stackoverflow.com/questions/70031167/event-type-typescript-for-event-handler-in-svelte
    const target = (event.target as HTMLInputElement);
    display += target.innerHTML;
  }

  function handleClear() {
    display = '';
  }

  function handleBackspace() {
    display = display.slice(0, -1);
  }

  function handleEqual() {
    try {
      display = eval(display);
    } catch (error) {
      display = 'Error';
    }
  }
</script>

<div id="calculator">
  <input type="text" bind:value={display}>
  <div class="clear-row">
    <button id="clear" on:click={handleClear}>C</button>
    <button id="backspace" on:click={handleBackspace}>CE</button>
  </div>
  <div class="number-row">
    <button id="7" on:click={handleClick}>7</button>
    <button id="8" on:click={handleClick}>8</button>
    <button id="9" on:click={handleClick}>9</button>
    <button id="divide" on:click={handleClick}>/</button>
  </div>
  <div class="number-row">
    <button id="4" on:click={handleClick}>4</button>
    <button id="5" on:click={handleClick}>5</button>
    <button id="6" on:click={handleClick}>6</button>
    <button id="multiply" on:click={handleClick}>*</button>
  </div>
  <div class="number-row">
    <button id="1" on:click={handleClick}>1</button>
    <button id="2" on:click={handleClick}>2</button>
    <button id="3" on:click={handleClick}>3</button>
    <button id="subtract" on:click={handleClick}>-</button>
  </div>
  <div class="number-row">
    <button id="0" on:click={handleClick}>0</button>
  <button id="decimal" on:click={handleClick}>.</button>
  <button id="add" on:click={handleClick}>+</button>
  <button id="equals" on:click={handleEqual}>=</button>
  </div>
</div>

<style>
#calculator {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  height: 500px;
  width: 400px;
  margin: 50px auto;
  background-color: #ddd;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #999;
}

input[type="text"] {
  height: 50px;
  width: 100%;
  font-size: 20px;
  text-align: right;
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 5px;
  border: none;
  box-shadow: 0 0 10px #999;
}

button {
  height: 50px;
  width: 50px;
  font-size: 20px;
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: #fff;
  box-shadow: 0 0 10px #999;
}

.clear-row {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.number-row {
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin-top: 10px;
}

button:hover {
  cursor: pointer;
  background-color: #ddd;
}

</style>