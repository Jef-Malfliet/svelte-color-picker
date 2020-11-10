<script>
  let r = 0;
  let g = 0;
  let b = 0;

  function componentToHex(c) {
    if (c == null) return "00";
    var hex = c.toString(16);
    return hex.length == 1 ? "0" + hex : hex;
  }

  let hexvalues = [
    "0",
    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
    "9",
    "A",
    "B",
    "C",
    "D",
    "E",
    "F",
  ];

  function inverseHex(s) {
    let values = [s.substr(0, 2), s.substr(2, 2), s.substr(4, 5)];
    let inverse = "";
    for (let i = 0; i < values.length; i++) {
      let indexfirst = hexvalues.indexOf(values[i].charAt(0));
      let indexsecond = hexvalues.indexOf(values[i].charAt(1));
      inverse += hexvalues[15 - indexfirst];
      inverse += hexvalues[15 - indexsecond];
    }
    return inverse;
  }

  $: hexValue = (
    "#" +
    componentToHex(r) +
    componentToHex(g) +
    componentToHex(b)
  ).toUpperCase();
  $: inverseHexValue =
    "#" + inverseHex(hexValue.substr(1, hexValue.length).toUpperCase());
</script>

<style>
  #result {
    width: 30em;
    height: 30em;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1px solid #eee;
    border-radius: 0.5em;
  }

  #wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #inputs {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 5em;
  }

  #top {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 98vh;
  }

  .slider {
    display: flex;
    align-items: baseline;
  }

  .button {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .color_value {
    margin: 0.5em;
  }

  input {
    margin: 0.4rem;
  }

  hr {
    border: 0;
    border-top: 1px solid #eee;
    margin: 20px -16px;
  }

  .div_hex {
    width: 5.4em;
	display: inline-block;
  }
</style>

<div id="top">
  <div>
    <h1>
      The
	  <span style="color: {hexValue};">background </span>
	  <div class="div_hex" style="color: {hexValue};">({hexValue})</div>
      and
	  <span style="color: {inverseHexValue};">text </span>
	  <div class="div_hex" style="color: {inverseHexValue};">({inverseHexValue})</div>
      have inverted colors
    </h1>
  </div>
  <div id="wrapper">
    <div id="result" style="background-color: rgb({r}, {g}, {b});">
      <h1 style="color: {inverseHexValue};">{hexValue}</h1>
    </div>
    <div id="inputs">
      <section>
        <div class="slider">
          <input type="range" id="red" min="0" max="255" bind:value={r} />
          <label for="red" class="color_value">R:
            <input type="number" bind:value={r} min="0" max="255" /></label>
        </div>
        <div class="slider">
          <input type="range" id="green" min="0" max="255" bind:value={g} />
          <label for="green" class="color_value">G:
            <input type="number" bind:value={g} min="0" max="255" /></label>
        </div>
        <div class="slider">
          <input type="range" id="blue" min="0" max="255" bind:value={b} />
          <label for="blue" class="color_value">B:
            <input type="number" bind:value={b} min="0" max="255" /></label>
        </div>
      </section>
      <hr />
      <section>
        <div class="button">
          <button
            on:click={() => {
              r = Math.floor(Math.random() * Math.floor(256));
              g = Math.floor(Math.random() * Math.floor(256));
              b = Math.floor(Math.random() * Math.floor(256));
            }}>Random Color!</button>
        </div>
      </section>
    </div>
  </div>
</div>
