# Computational Modeling in Neuroimaging
# 1. Mesh Representation of Brain Anatomy
| Learning Goals |         
|----------------|
|<ul><li>Digital voxels, cuboids, boundary</li></ul> |
|<ul><li>Well-composedness of voxel boundaries </li></ul>|
|<ul><li>**Triangular mesh:** vertices, faces, edges </li></ul>|
|<ul><li>**Topology:** Euler number, genus</li></ul> |
|<ul><li>Mesh Reconstruction</li></ul>  |
|<ul><li>Well-composed boundaries </li></ul>|
|<ul><li>Generation of smooth mesh representations</li></ul>|



**Digital Representation of MR Images:**  
To start thinking about the digital representation of an MR image,  
start with visualizing a lattice of size IxJxK.  

![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/5985e589-c9ea-4401-9f2b-753d20fbdb1b)


- Voxel: each point in the lattice
  
|MR Image  | Functions defined over the grids |
|--------- | -------------------------------- |
|T1 & T2   | scalar values |
|Diffusion | vectors |
|Functional MRI |  time series | 

|Spatial Resolution | RAS coordinate system      |
|------------------ | -------------------------- |
|hx, hy, hz         | X+: Right; Y+: Anterior; Z+: Superior |
| ![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/9ee7a7fe-0e1d-4c38-86b6-6ddd620611bf)| ![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/332b5427-04f5-4469-8778-09d13e5558b9) |

Cuboids for p=(i,j,k):
- The set C(p) represents the points (x, y, z) that lie within the cuboid.
- The cuboid is centered at the point p = (i, j, k).
- The half-lengths of its sides are denoted as h₁/2, h₂/2, and h₃/2.
- Mathematically, the set C(p) consists of points that satisfy the following conditions:  
![image](https://github.com/Liz-Neuroimaging-Notebook/testpageforNIIN550/assets/156251670/afd25d66-d138-4e7a-be8a-ffd8b6cb636c)  



#### Triangular Mesh Representation
- By dividing each cuboid face into two triangles, we obtain a triangular mesh representation of boundaries
- A mesh is composed of: vertices, faces, edges, angles

#### Mesh Topology  
- Euler number: X = V+F-E V=number of vertices; F=number of faces; E=number of edges  
- Genus of meshes: g = number of holes  
- Relations between Euler number and g, X=2-2g  
- **Most common brain surfaces: genus-zero (spherical) topology**

|    g=0                |        g=2                |
|-----------------------|---------------------------|
|![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/8e7aed22-d6c0-4a4b-a5e6-239dcce37bd0)|![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/d85349d4-e0a5-4f66-a1b6-36b26a3626ea)|


Assignment: 
Let I denote an MRI image of size 256x256x256 with an isotropic resoluRon of 1mm. All the voxels are stored in the RAS orientaRon. Let p = (1,1,1) denote the voxel with a coordinate (1,1,1). 



# 2.Curvature 
| Learning Goals |         
|----------------|
| <ul><li>Continuous and discrete definition of curves</li></ul>|
| <ul><li>Mathematical definition of tangent, normal, binormal, and curvature of curves</li></ul> |
| <ul><li>Discrete calculation of curvatures on curves in MATLAB</li></ul>   |
| <ul><li>Principal curvatures on surface</li></ul>  |
| <ul><li>Mean and Gaussian curvatures</li></ul>  |
| <ul><li>Shape index </li></ul>|

-Curvature describes the “curvedness” of shapes  
-Surface: how fast it deviates from a plane  
-Widely used for the geometric modeling of neuroanatomy  
-It is a local measure

### Curves ≠ Curvature 
- The curvature of a surface is defined according to the curvature of curves
- Curves are by themselves useful geometric models in brain imaging,
for example, as seen in:
  
| Sulcal lines on cortical surfaces  |   Fiber tracts from tractography  |
|------------------------------------|-----------------------------------|
|![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/e721ca8d-f5a2-4dff-b833-be77072337d0)|![image](https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/e99bab6e-d3d4-4a25-81f1-66423d3634e3)|


| Curve    |  vs  |  Polyline   | 
|----------|------|-------------|
|A map from the real line to the 3D space, i.e., a curve C is parameterized by t∈R, and every point C(t)∈𝑅^3If C(t)∈𝑅^2, it is a planar curveIf C(a)=C(b), it is a closed curve. Special case: t is the arc length of the curve.edit/main/README.md  |      | A polyline is a discrete and ordered set of points in 𝑅^3. In MATLAB, it is an array of size Nx3. N: number of points in the polyline Resample to segments of equal lengt Two vectors a and b, the length is norm(a-b).|
|<img src="https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/a68de2f7-7d85-4f05-b492-6b83eb1bf9a2" width="200" height="200"/>| | <img src="https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/548e76ca-b152-4701-8087-0804b4b329cb" width="150" height="150" /> <img src="https://github.com/Liz-Neuroimaging-Notebook/Computational-Modeling-in-Neuroimaging/assets/156251670/fee41c15-db15-4921-bd77-f3e0b6a19e31" width="150" height="150" />|


