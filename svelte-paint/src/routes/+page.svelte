<script>
    let drawing = false;
    let color = '#000000';
    let lineWidth = 3;
    let isErase = false;
    let ctx;
    let canvas;
  
    const handleMouseDown = () => {
      drawing = true;
    };
  
    const handleMouseUp = () => {
      drawing = false;
    };
  
    const handleClear = () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    };
  
    const handleColorChange = (e) => {
      color = e.target.value;
    };
  
    const handleLineWidthChange = (e) => {
      lineWidth = e.target.value;
    };
  
    const handleErase = () => {
      if (isErase) {
        color = '#FFFFFF';
      } else {
        color = '#000000';
      }
      isErase = !isErase;
    };
  
    const handleMouseDownCanvas = (event) => {
      handleMouseDown();
      const { offsetX, offsetY } = event;
      ctx = canvas.getContext('2d');
      ctx.strokeStyle = color;
      ctx.lineWidth = lineWidth;
      ctx.beginPath();
      ctx.moveTo(offsetX, offsetY);
    };
  
    const handleMouseMoveCanvas = (event) => {
      if (!drawing) return;
      const { offsetX, offsetY } = event;
      ctx.lineTo(offsetX, offsetY);
      ctx.stroke();
    };
  
    const handleMouseUpCanvas = (event) => {
      handleMouseUp();
      ctx.closePath();
    };
  </script>
  
  <div>
    <p>Welcome to your canvas!</p>
    <div>
      <input type="color" bind:value={color} on:change={handleColorChange} />
      <input type="range" min="1" max="15" bind:value={lineWidth} on:change={handleLineWidthChange} />
      <button on:click={handleClear}>Clear</button>
      <button on:click={handleErase}>{isErase ? 'Erase' : 'Draw'}</button>
    </div>
    <canvas
      width="800"
      height="600"
      on:mousedown={handleMouseDownCanvas}
      on:mouseup={handleMouseUpCanvas}
      on:mousemove={handleMouseMoveCanvas}
      style="border: 1px solid black"
      bind:this={canvas}
    />
  </div>