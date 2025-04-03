---
title: "GPUComputePassEncoder: dispatchWorkgroupsIndirect() Methode"
short-title: dispatchWorkgroupsIndirect()
slug: Web/API/GPUComputePassEncoder/dispatchWorkgroupsIndirect
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{APIRef("WebGPU API")}}{{SeeCompatTable}}{{SecureContext_Header}}{{AvailableInWorkers}}

Die **`dispatchWorkgroupsIndirect()`** Methode der [`GPUComputePassEncoder`](/de/docs/Web/API/GPUComputePassEncoder) Schnittstelle dispatcht ein Raster von Arbeitsgruppen, das durch die Parameter eines [`GPUBuffer`](/de/docs/Web/API/GPUBuffer) definiert wird, um die Arbeit auszuführen, die von der aktuellen [`GPUComputePipeline`](/de/docs/Web/API/GPUComputePipeline) durchgeführt wird (d.h. gesetzt über [`GPUComputePassEncoder.setPipeline()`](/de/docs/Web/API/GPUComputePassEncoder/setPipeline)).

## Syntax

```js-nolint
dispatchWorkgroupsIndirect(indirectBuffer, indirectOffset)
```

### Parameter

- `indirectBuffer`

  - : Ein [`GPUBuffer`](/de/docs/Web/API/GPUBuffer), der die X-, Y- und Z-Dimensionen des Rasters von Arbeitsgruppen enthält, die zu dispatchen sind. Der Puffer muss einen eng gepackten Block aus drei 32-Bit-Integer-Werten enthalten, die die Dimensionen darstellen (insgesamt 12 Bytes), in der gleichen Reihenfolge wie die Argumente für [`GPUComputePassEncoder.dispatchWorkgroups()`](/de/docs/Web/API/GPUComputePassEncoder/dispatchWorkgroups). Ein Beispiel:

    ```js
    const uint32 = new Uint32Array(3);
    uint32[0] = 25; // The X value
    uint32[1] = 1; // The Y value
    uint32[2] = 1; // The Z value

    // Write values into a GPUBuffer
    device.queue.writeBuffer(buffer, 0, uint32, 0, uint32.length);
    ```

- `indirectOffset`
  - : Der Offset in Bytes, ab dem im `indirectBuffer` die Dimensionsdaten beginnen.

> [!NOTE]
> Die X-, Y- und Z-Dimensionswerte, die an [`GPUComputePassEncoder.dispatchWorkgroups()`](/de/docs/Web/API/GPUComputePassEncoder/dispatchWorkgroups) und `dispatchWorkgroupsIndirect()` übergeben werden, sind die Anzahl der zu dispatchenden Arbeitsgruppen für jede Dimension, nicht die Anzahl der Shader-Ausführungen, die über jede Dimension durchgeführt werden sollen. Dies entspricht dem Verhalten moderner nativer GPU-APIs, unterscheidet sich jedoch vom Verhalten von OpenCL. Das bedeutet, dass wenn ein [`GPUShaderModule`](/de/docs/Web/API/GPUShaderModule) einen Einstiegspunkt mit `@workgroup_size(4, 4)` definiert und die Arbeit mit dem Aufruf `dispatchWorkgroupsIndirect(indirectBuffer);` dispatcht wird, wobei `indirectBuffer` X- und Y-Dimensionen von 8 und 8 angibt, der Einstiegspunkt insgesamt 1024 Mal ausgeführt wird — 8 Mal entlang sowohl der X- als auch der Y-Achsen wird eine 4 x 4 Arbeitsgruppe dispatcht. `4 * 4 * 8 * 8 = 1024`.

### Rückgabewert

Keiner ({{jsxref("Undefined")}}).

### Validierung

Die folgenden Kriterien müssen erfüllt sein, wenn **`dispatchWorkgroupsIndirect()`** aufgerufen wird, andernfalls wird ein [`GPUValidationError`](/de/docs/Web/API/GPUValidationError) generiert und der [`GPUComputePassEncoder`](/de/docs/Web/API/GPUComputePassEncoder) wird ungültig:

- `indirectBuffer`'s [`GPUBuffer.usage`](/de/docs/Web/API/GPUBuffer/usage) enthält das `GPUBufferUsage.INDIRECT` Flag.
- `indirectOffset` + die durch die `X`, `Y` und `Z` Dimensionen angegebene Gesamtgröße ist kleiner oder gleich der [`GPUBuffer.size`](/de/docs/Web/API/GPUBuffer/size) des `indirectBuffer`.
- `indirectOffset` ist ein Vielfaches von 4.

## Beispiele

```js
// Set global buffer size
const BUFFER_SIZE = 1000;

// Compute shader; note workgroup size of 64
const shader = `
@group(0) @binding(0)
var<storage, read_write> output: array<f32>;

@compute @workgroup_size(64)

...

`;

// ...

// Create GPUCommandEncoder to encode commands to issue to the GPU
const commandEncoder = device.createCommandEncoder();

// Initiate render pass
const passEncoder = commandEncoder.beginComputePass();

// Issue commands
passEncoder.setPipeline(computePipeline);
passEncoder.setBindGroup(0, bindGroup);

const uint32 = new Uint32Array(3);
// Note workgroupCountX is set based on the global buffer size and the shader workgroup count.
uint32[0] = Math.ceil(BUFFER_SIZE / 64);
uint32[1] = 1;
uint32[2] = 1;

const workgroupDimensions = device.createBuffer({
  size: 12,
  usage: GPUBufferUsage.COPY_DST | GPUBufferUsage.INDIRECT,
});
device.queue.writeBuffer(workgroupDimensions, 0, uint32, 0, uint32.length);

passEncoder.dispatchWorkgroupsIndirect(workgroupDimensions, 0);

// End the render pass
passEncoder.end();

// Copy output buffer to staging buffer
commandEncoder.copyBufferToBuffer(
  output,
  0, // Source offset
  stagingBuffer,
  0, // Destination offset
  BUFFER_SIZE,
);

// End frame by passing array of command buffers to command queue for execution
device.queue.submit([commandEncoder.finish()]);

// ...
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- Die [WebGPU API](/de/docs/Web/API/WebGPU_API)
