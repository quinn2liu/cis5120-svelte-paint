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
  
    const handleColor = (e) => {
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
  
  <div style="display: flex; flex-direction: column; align-items: center; margin-top: 1rem;">
    <p style="font-family: Arial, sans-serif; font-size: 20px; font-weight: bold;">Welcome to your canvas!</p>    <div style="padding-bottom: 20px;">
        <input type="color" bind:value={color} on:change={handleColor} />
        <input type="range" min="1" max="15" bind:value={lineWidth} on:change={handleLineWidthChange} />
        <button 
        style="padding: 8px; background-color: #fc8181; border-radius: 6px; border-color: #fc8181; font-family: Arial, sans-serif; font-weight: 600;"
        on:click={handleClear}>Clear</button>
        <button 
        style="padding: 8px; background-color: #68D391; border-radius: 6px; border-color: #fc8181; font-family: Arial, sans-serif; font-weight: 600;"
        on:click={handleErase}>{isErase ? 'Erase' : 'Draw'}</button>
    </div>
    <canvas
        width="800"
        height="600"
        on:mousedown={handleMouseDownCanvas}
        on:mouseup={handleMouseUpCanvas}
        on:mousemove={handleMouseMoveCanvas}
        style="border: 1px solid black; padding-top: 10px; border-radius: 12px"
        bind:this={canvas}
    />
  </div>
  