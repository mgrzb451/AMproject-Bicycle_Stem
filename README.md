# Bicycle Stem DfAM Conforming Project

Let's lean more heavily into Additive Manufacturing's capabilities and design a Bicycle Stem leveraging Simcenter NX's Topology Optimization and Lattice Designer tools. Let's see if we can create something better than current market offerings! 😀

<img width="393" height="410" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/0.jpg" />


## Design Requirements

- Material for the Stem will be **Ti-6Al-4V**, Laser Powder Bed Fusion will be used
  
  - `Re = 950 MPa | Rm = 1050 MPa`
- The part will be validated through FEA
  
  - **ISO 4210-5 Static Test** - `1 kN` of Force applied vertically at the handlebar bore centerline, `50 mm` from the stem midplane
- Additional load case will be performed
  
  - Emergency Braking - A `90 kg` rider braces against a deceleration of `0.8 g`. `FoS of 1.35` will be assumed
    
  - `Vertical force = 0.50 (of rider mass) × 90 (rider mass) × 9.81 (g) = 441 N`
    
  - `Horizontal force = 0.8 (deceleration) × 90 (rider mass) × 9.81 (g) × 0.35 (of rider mass) = 441 N`
    
- For all tests an Endurance Limit of `Se = 540 MPa` for $10^{7}$ cycles with an FoS will be assumed as the Stress Limit
  

# Iterative Topology Optimization

Multiple iterations of geometry optimization were performed. Each Iteration included a combination of Load Subcases described earlier. After each iteration the Design Space was evaluated and adjusted based on the achieved results.

<img width="1323" height="702" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/1.jpg" />


## Final Optimized Geometry

<img width="1359" height="551" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/2.jpg" />


# 3D Design

Based on the final optimized geometry created by TO we manually design a part for 3D printing, taking into account the chosen AM processes' limitations and keeping all the best DfAM practices in mind.

<img width="1200" height="512" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/3.jpg" />


The bores for the Steerer Column and Handlebars will be Reamed to the precise dimensions required. As printed holes for bolts will be drilled to remove the machining allowance and create smooth surfaces. The split-cuts will be sawn.

<img width="1545" height="512" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/4.jpg" />


Leveraging AM allowed us to also consolidate the assembly structure of a standard, multipart Bicycle Stem into a single component. We reduced manufacturing complexity, saved weight, saved 💰 on packaging and simplified assembly and operation for the users!

<img width="1224" height="505" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/4a.jpg" />


## Lattice Structure

We'll use this opportunity to explore the Lattice Designer Application in Simceneter. Let's replace the solid struts with an organic Lattice. Based on the geometry, process requirements and limitations and the cool factor 😎 I've chosen a **Voronoi Lattice** with a Gradient of porosity conforming to the geometry.

Looks awesome!

### Interactive 3D
Click the image 😃

<a href="https://skfb.ly/pHGML">
  <img width="317" height="259" alt="image" src="https://github.com/user-attachments/assets/0bd3cee6-a964-45bc-8ccf-d734c7f10d1f" />
</a>

<hr>

<img width="954" height="727" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/5.jpg" />
<img width="1152" height="809" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/6.jpg" />
<img width="748" height="205" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/7.jpg" />


# FEA

The Lattice Geometry requires a very fine mesh which my ancient PC will struggle with so we'll limit the FEA to the **ISO 4210-5 Static Test** required for homologation of the part. We'll try to make the set-up as realistic as possible though, by utilizing contact with rigid 2D Shell meshed Surfaces that will provide support and load application and transfer targets. We modify several Nastran parameters to aid Contact Convergence and ease the computation requirements.

<img width="986" height="696" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/8.jpg" />
<img width="880" height="489" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/9.jpg" />


## Results

The **ISO 4210-5 Static Test** requires the part doesn't deform by more than `3 mm` in response to the applied load. I'd say we aced that requirement 💪🏻

<img width="1816" height="820" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/disp.gif" />

I do have a problem with the Stress results. While we are below our strict `540 MPa` stress limit we imposed, we're close to it. The problem I have is that the high values are isolated to singular nodes. Even adjacent nodes on the same element show values lower by 100 MPa. I think the high values are results of sharp geometry in the lattice that create artificial stress concentrations.

<img width="860" height="751" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/10.jpg" />
<img width="898" height="770" alt="image" src="https://github.com/mgrzb451/AMproject-Bicycle_Stem/blob/main/assets/11.jpg" />


# Conclusions

- Adding contact to FEA drastically increases the computation costs of the analysis *sad emoji*

- Lattice structure creates very fine features, often resulting in artificial stress concentration points that make FEA results hard to interpret. Building a physical prototype and performing real world test would be required to make sure the performed analyses yield accurate results.

- Additive Manufacturing enables use of Lattice Structures which are incredible in terms of performance to weight ratio and I truly believe AM is the future of manufacturing!

- Based on my current skills, raw geometry output by the Topology Optimization software isn't really suitable to just be printed as is. And the process of manually creating an optimized CAD model based on those results is incredibly fun and challenging but quite demanding in terms of modeling skills and time investment

- I am very excited to learn more specialized TO software like nTOP in the near future! 😃
