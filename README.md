# Computer Graphics Final Project

A renderer developed as part of the Computer Graphics Final Project. This project focuses on implementing key rendering techniques to simulate realistic lighting and post-processing effects.

## Features Implemented

### Rendering Core
- **BVH Traversal**  
  Efficient acceleration structure for ray-scene intersection.

- **Shading Model Comparison**  
  Implemented and evaluated multiple shading model to compare visual results.

### 💡 Lighting & Shadows
- **Segment Light Sampling**  
  Custom light sampling for linear/area light sources.

- **Parallelogram Light Sampling**  
  Simulation of soft shadows and realistic falloff.

- **Transparency Handling**  
  Visibility computation through transparent surfaces.

### Post-Processing
- **Bloom Filter**  
  Simulates light bleeding for overexposed areas in the scene.

- **Depth of Field**  
  Applies camera-like blur effects based on object distance from the focal plane.
