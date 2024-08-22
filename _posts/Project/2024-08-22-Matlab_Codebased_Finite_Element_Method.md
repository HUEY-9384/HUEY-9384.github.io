
Matlab Code based Finite Element Method

#

First Name: Hyungsuk


Last Name: Seo

Initials: HS


* * *

Table of Contents

[Abstract        2](#h.kq8wyn7uyv3g)

[Introduction        2](#h.lk2qrme096x)

[Task 1. Initializing FEM model and dividing nodes        3](#h.755ipsylakbr)

[Initializing fem model        3](#h.9l8zg34abcax)

[Algorithm        3](#h.igt1wox8bh8d)

[Dividing node processing        4](#h.6k84x9y3thv7)

[Algorithm        5](#h.lid8gf2v9qia)

[The results        6](#h.trm0yx9dii59)

[Initial model From NX CAD        7](#h.w8yp75np73dp)

[Task 2. Torsion Stiffness and Rotational degrees        8](#h.it3d4kbymdg1)

[The results        9](#h.mqyuaunzoxtv)

[Task 3 compare between NX CAD and matlab based FEM        10](#h.bbif5v5q66jg)

[Results        10](#h.u55j1x734jx3)

[Reference        11](#h.wz6l1583gr60)

[References        11](#h.redjrd46qo4b)

[Appendix        11](#h.jbzbvfsivok9)

* * *

Abstract
========

This project was initiated based on my previous Automotive Structure Design project and the MATLAB coding I developed during a FEM project. This project goal is to rewrite the MATLAB code to address the errors and issues that had arisen in earlier versions. One of the key advantages of using MATLAB for FEM analysis is its ease in configuring nodes and elements, the flexibility to set material properties, and the ability to perform optimization more effectively than traditional CAD programs. After rewriting the MATLAB code, I compared the torsional stiffness and rotational outcomes with those obtained from NX CAD and matlab-based FEM. This comparison was intended to evaluate the practicality of MATLAB in FEM analysis. The results showed a 10.10% error difference between the MATLAB-based FEM and the NX CAD FEM. Although this indicates some discrepancies, it also suggests that MATLAB remains a practical tool for FEM analysis.
Introduction
============

This project utilizes the structure of a sedan frame from previous projects. The objective is to determine the torsional stiffness of this structure (see Figure 1) using the Finite Element Analysis (FEA) method, implemented in both MATLAB code and NX CAD. All relevant information, including length, thickness, side length, density, joints, coordinates, and forces, is provided from previous project instructions.Task 1 involves creating an initial model using MATLAB. After initializing the FEA model, the structure is divided into nodes for analysis. Task 2 focuses on finding the torsional stiffness and the degree of rotation using MATLAB-based FEM. Task 3 compares the results of the MATLAB-based FEM analysis with those obtained from the NX CAD-based FEM analysis.

![](images/image19.png)

Figure.1 structure of sedan

Task 1. Initializing FEM model and dividing nodes
=================================================

Initializing fem model
----------------------

Coordinates were given in table.1. Nodes were connected Based on table.1, nodes connected and combined as elements then plotted(figure 2).

![](images/image11.png)

Figure.2: plotted after connected elements( number is refer to number of elements)

### Algorithm

Algorithm of plotting this structure is very simple.define number of elements using length or size. The looping process is Using a while loop  number of elements times and using plot3(node x 1:2, nodes y 1:2, node z 1:2).

![](images/image18.png)

Figure.3: algorithm of plotting

 Dividing node processing
-------------------------

Diving nodes is very important in FEM. Because, usually more nodes have more accuracy. However, it will increase computing time and may result in inaccurate results due to code and program issues.

Dividing nodes instructure is below:

Each structural beam in Figure2 needs to be modeled by several finite element beam elements. The length of all middle beam elements for each beam structure should be 0.1 m. The length of the start and the end elements for each structural beam should be equal to each other and the maximum of their length should be 0.05 m(see figure 4).

![](images/image8.png)![](images/image15.png)

   Figure 4: example of dividing nodes

Divided nodes need L , m,n.l and d are required. L is the length of an element. m,n,l,D are the directions of cosines  xyz.  m,n,i,D will be the same as the original element. Because new nodes are under original elements.

![](images/image6.png)

Figure 5: l,m,n

### Algorithm

Algorithms of the coding process can see figure 6. Which means that try to divide 0.1 first if there is any reminder then L\_n2divider will be reminder divide by 2. Then counts how many divide-able,  total divider is total elements going to add in elements.

![](images/image4.png)

Figure 6: algorithm of coding for dividing nodes process

After adding new nodes, we need to reconnect the original to new nodes.  The algorithm of the connecting process is figure 7.

![](images/image14.png)

Figure 7: algorithm of connect process

 The results
------------

After this the same algorithm is used for plotting. Result is in figure 8

![](images/image7.png)

Figure 8: result of divided nodes, each line of color is elements, blue circle is adjacent nodes.

Initial model From NX CAD
-------------------------

The initial model is based on the provided parameters in the project. The material properties (provided parameters) are as follows:

| **Material Property**        | **Value**        |
|------------------------------|------------------|
| Young’s Modulus, E           | 206 GPa          |
| Shear Modulus, G             | 79.85 GPa        |
| Poisson’s Ratio              | 0.29             |
| Density                      | 7850 kg/m³       |
| Yield Strength               | 310 MPa          |
 


Based on this data, a CAD and FEA model was produced and used for all future deliverables up to Milestone 3, where a redesign of the beams is outlined as scope. The following was replicated in Siemens NX.

![](images/image16.png)

Figure 9: Provided Beam Frame Car Structure (Sedan)

![](images/image3.png)

Figure 10: our initial structure setup

![](images/image5.png)

Figure 11: Initial force setup

Task 2. Torsion Stiffness and Rotational degrees
================================================

Initial vehicle Torsion stiffness is how much the car is twisted by forcing acting on suspension.

It must be higher than suspension stiffness. If it is less than suspension stiffness, suspension will not function properly.  Calculate Ts = Initial Vehicle Torsion Stiffness needs a lot of information needed. But the basic formula is in eq\[1\]. T is torque acting on node 5 and 6. T can be calculated F\*L

L is the length of width of the car F is the force that I sat on. T can also find total nodal forces acting in the Z direction of  node 5 or node 6 and multiply L. ![](images/image1.png) is the degree of torsion of structure. It can be found from displacement is calculated from global matrix. which I stored in variable d

![](images/image2.png)                                                \[1\]

To find the global matrix, we need to find thease Ix,Iy,Iz, K’, lambda, Transformation matrix, E,G,J. E and G are given in the project manual. I already formed and calculated these from a previous project.

The results
-----------

Results Ts1=78410 Nm/deg, maximum rotational degree is 0.0097deg. Figure 12 is deflection of the structure by 1000 more gained result

![](images/image12.png)

Figure 12 : 1000 gained from original result

Result from NX CAD Ts1= 86019.19Nm/deg, maximum rotational degree is 0.008719 deg. Figure 13 simulation result 10% more deflected plot. Figure 14  is data results simulated  100N to 1000N.

![](images/image17.png)

Figure 13: Example results force at 1000N

![](images/image13.png)

Figure 14: Data for pure torsion K is torsion stiffness

Task 3 compare between NX CAD and matlab based FEM
==================================================

Compared between NX CAD results and Matlab based FEM , I found that TS1 has 8.85% and Deg has 10.10% errors. This could be potentially issued for validation. However, It delivers decent performance.

Table.1

| **Parameter** | **NX**       | **MATLAB**  | **Error**  |
|---------------|--------------|-------------|------------|
| Ts1           | 86019.014    | 78410       | 8.85%      |
| Deg           | 0.008719     | 0.0097      | 10.10%     |


Results
=======

Results Ts1=78410 Nm/deg,  from NX CAD Ts1= 86019.19Nm/deg maximum rotational degree is 0.0097deg, for NX CAD maximum rotational degree is 0.008719 deg. There are 8.85 errors between NX cad and matlab based code and 10.10% difference rotational degree.

Reference
=========

References
==========

\[1\] MECE4290U Finite Element Methods lecture 10  

, Ontario Tech University Faculty of Engineering and Applied Science.

\[2\]MECE4290U Finite Element Methods Tutorial 8  

, Ontario Tech University Faculty of Engineering and Applied Science.

\[3\]MECE4290U Finite Element Methods Tutorial 6  

, Ontario Tech University Faculty of Engineering and Applied Science.

\[4\]MECE4290U Finite Element Methods Tutorial 8  

, Ontario Tech University Faculty of Engineering and Applied Science.

\[5\]D. Krzikalla, J. Mesicek, J. Petru, A. Sliva, and J. Smiraus, “Walshmedicalmedia,” Journal of Applied Mechanical Engineering, 07-Jan-2019. \[Online\]. Available: https://www.walshmedicalmedia.com/open-access/analysis-of-torsional-stiffness-of-the-frame-of-a-formula-student-vehicle-31847.html. \[Accessed: 23-Nov-2022\].

\[6\]L. D. L., A first course in the finite element method, 6th ed. Stamford, C: Cengage Learning, 2017.

page 986, and page 295

\[7\]“Welcome to Chalmers Library!,” Visa webbsidan på svenska. \[Online\]. Available: https://www.lib.chalmers.se/en/. \[Accessed: 23-Nov-2022\].

Appendix
========

Coordinates backup

nodesL= \[ 0 0.6 0.25

 0 -0.6 0.25

 0 0.75 0.45

 0 -0.75 0.45

 0.375 0.75 0.58

 0.375 -0.75 0.58

 1.05 0.75 0

 1.05 -0.75 0

 1.05 0.75 0.63

 1.05 -0.75 0.63

 1.55 0.75 0

 1.55 -0.75 0

 1.5 0.65 1.18

 1.5 -0.65 1.18

 2.15 0.75 0

 2.15 -0.75 0

 2.15 0.75 0.9

 2.15 -0.75 0.9

 2.1 0.65 1.28

 2.1 -0.65 1.28

 2.7 0.65 1.28

 2.7 -0.650 1.28

 2.8 0.75 0

 2.8 -0.75 0

 3.2 0.75 0.23

 3.2 -0.75 0.23

 3.2 0.65 1.1

 3.2 -0.65 1.1

 3.6 0.75 0.73

 3.6 -0.75 0.73

 3.65 0.75 0.28

 3.65 -0.75 0.28

 4.1 0.75 0.33

 4.1 -0.75 0.33

 4.1 0.75 0.73

 4.1 -0.75 0.73\];

elements=\[1 3

    2 4

    1 7

    2 8

    3 5

    4 6

    5 9

    6 10

    7 11

    8 12

    11 15

    12 16

    7 9

    8 10

    9 13

    10 14

    13 19

    14 20

    15 23

    16 24

    15 17

    16 18

    17 19

    18 20

    19 21

    20 22

    21 27

    22 28

    23 25

    24 26

    25 27

    26 28

    27 29

    28 30

    25 31

    26 32

    29 35

    30 36

    31 33

    32 34

    33 35

    34 36

    7 8

    9 10

    11 12

    13 14

    15 16

    23 24

    25 26

    27 28

    29 30

    33 34\];

![](images/image10.png)

![](images/image9.png)