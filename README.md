<h1 align="center">Computer Graphics Final Project - Ray Traced Renderer</h1>

<p align="center">
A <b>ray-traced renderer</b> developed as part of the Computer Graphics Final Project.<br/>
The project explores <b>rendering techniques</b>, <b>lighting models</b>, <b>shadows</b>, and <b>post-processing effects</b>.
</p>

---

## Features  

### BVH Traversal  
Efficient acceleration structure for ray–scene intersections.  

---

### Shading Models  

Implemented and compared multiple shading models (**Phong**, **Blinn-Phong**, and custom **Linear Gradient shading**).  

**Linear Gradient Sampling**  
Use linear interpolation to sample colors from gradient based on given parameter *t*.  

<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Linear_Gradient_Model.png" width="400"/>
</p>

**Comparison Model**  
Highlights differences between Phong and Blinn-Phong specular components, sampling gradients based on normalized differences.  

<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Comparison-Model.png" width="350"/>
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Comparison-Model-(Different%20View).png" width="350"/>
</p>

**Visual Debug**  
- Red -> Phong dominant (sharp intense highlights)  
- Cyan -> Blinn-Phong dominant (broader softer highlights)  
- Gray -> Similar contribution  

---

### Lights & Shadows  

Light contribution and shadow handling for point, segment, and parallelogram lights.  
Visibility is calculated using binary or transparency-based methods.  

Visibility True (Green Ray)  
The ray reaches the light without obstruction.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Visibility(True).png" width="450"/>
</p>

Visibility False (Red Ray)  
The ray is blocked by an object.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Visibility(False).png" width="450"/>
</p>

Transparency Visibility  
Rays partially pass through transparent objects, producing softer shadows with color blending.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Transparency_Visibility_Ray.png" width="450"/>
</p>

---

## Segment Light (Many Samples)  

Multiple rays sampled along the light segment.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/SegmentLight_Uniform.png" width="600"/>
</p>

---

## Parallelogram Light  

Debug Visualization  
Red spheres indicate rays that cannot reach the light due to occlusion.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/ParallelogramLight.png" width="500"/>
</p>

Rendered Version  
The area light produces soft and realistic illumination.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/image30.jpg" width="500"/>
</p>

---

## Sampler Difference (64 Samples)  

Green -> Sample 2D  
Red -> Sample 1D for x and y  

Both approaches result in the same uniform distribution of samples.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Sampler_Diff(64%20samples).png" width="600"/>
</p>

---

### Bloom Effect  

A bloom effect applied via:  
1. Extracting bright pixels (threshold, mapping).  
2. Blurring with a separable Gaussian filter (binomial coefficients).  
3. Adding blurred highlights back to the scene.  

Mapping Functions: Binary · Linear · Exponential · Logarithmic · Sigmoid · Piecewise  

Example (Sigmoid Bloom)

<table align="center">
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Bloom.jpg" width="300"/><br/>
      <sub>Final Image (with Bloom)<br/>Scene after bloom is applied, bright areas glow with a smooth sigmoid falloff.</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Bloom_Only.jpg" width="300"/><br/>
      <sub>Only Bloom Contribution<br/>The blurred highlights layer extracted and only showed that part.</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Bloom_Only_GrayScale.jpg" width="300"/><br/>
      <sub>Only Bloom (Grayscale)<br/>Same bloom only layer with this time in grayscale to see intensity distribution clearly.</sub>
    </td>
  </tr>
</table>

---

### Depth of Field  

For each pixel, multiple rays are generated via `generateDepthOfFieldRays(...)`, which samples random points on the lens disk and directs rays toward a focal point based on a user-defined focal distance, image plane, and lens radius settings. Each ray accumulates color contributions, averaged to compute the final pixel color. The implementation uses the lens radius, focal distance, and camera orientation to simulate in-focus and out-of-focus regions, producing blurring effects for objects outside the focal plane.  

---

## Examples  

Fully Blurred Image  
All objects are outside the focal plane, producing uniform blur.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Fully_Blurred_Image.png" width="450"/>
</p>

Focused Green Box  
The green box lies on the focal plane, sharp and in focus. The red box is blurred in the background.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Focused_Green.png" width="450"/>
</p>

Focal Point Hitting the Triangle  
The focal point aligns exactly with the triangle, making it sharp while surroundings blur.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Focal_Point.png" width="450"/>
</p>

Focal Plane Visualization  
Green = Focal Plane, Blue = Image Plane, Red Ellipse = Thin Lens.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Focal_Plane.png" width="500"/>
</p>

Focal Plane Sampling  
Yellow spheres represent grid points sampled on the focal plane for depth-of-field ray generation.  
<p align="center">
  <img src="https://raw.githubusercontent.com/KaanAres10/Computer-Graphics-Final-Project/web/doc/Yellow_Spheres.png" width="500"/>
</p>

---

## Reflection  

This project taught me:  
- How to implement a ray-traced rendering pipeline, from BVH traversal and ray–scene intersection to shading and post-processing.  
- How to design debug visualizations to compare shading models and light sampling.  

---

## Tech Stack  

- Languages: C++17, GLSL  
- Graphics API: OpenGL 4.5  
- Build System: CMake  
