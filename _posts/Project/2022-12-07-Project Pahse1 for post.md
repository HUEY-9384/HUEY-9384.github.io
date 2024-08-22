
![](images/image37.png)

FACULTY OF ENGINEERING AND APPLIED SCIENCE

MECE 4290U Finite Element Methods

Project 1 Phase 1

Course Instructor:         Professor. Ahmad Barari

#

First Name: Hyungsuk

Last Name: Seo

Student Number: 100697260

Initials: H.S



* * *

Table of Contents

[Abstract        1](#h.kq8wyn7uyv3g)

[Introduction        1](#h.lk2qrme096x)

[Task 1. Initializing FEM model and dividing nodes        3](#h.755ipsylakbr)

[Initializing fem model        3](#h.9l8zg34abcax)

[Coding        3](#h.igt1wox8bh8d)

[Dividing node processing        3](#h.6k84x9y3thv7)

[Coding        5](#h.lid8gf2v9qia)

[The results        5](#h.trm0yx9dii59)

[Task 2. Weight and Load        6](#h.it3d4kbymdg1)

[Coding        7](#h.zgrifgbr0fbc)

[The results        7](#h.9nal7iirbtt)

[Task 3.  Pure Torsion        8](#h.7tfl8gahguuu)

[Lambda        9](#h.r7r9ybrdd1ob)

[The results        9](#h.k6virtns1w92)

[Transformation        9](#h.3khfgzwybieo)

[The results        9](#h.ebzkntjpvimo)

[K’        10](#h.fjr47c62bghb)

[The results        10](#h.jkj7cac9wb0g)

[Global matrix        11](#h.4c8l95cl7c2p)

[The results        11](#h.odjtzjdzluqy)

[Initialize constrain and forces        11](#h.z28sgu3bobu1)

[The results        13](#h.tnn3m6qlf7df)

[Displacement        13](#h.13kqpbnp6wac)

[The results        14](#h.c0wru39s867l)

[Ts1        14](#h.7lswn0wrwpgs)

[The results        14](#h.mqyuaunzoxtv)

[Task 4 Torsion Study        15](#h.bbif5v5q66jg)

[The results        15](#h.k6xdm0nmt4ie)

[Discussion        16](#h.nk6msp26pt9t)

[Results        17](#h.u55j1x734jx3)

[Reference        17](#h.wz6l1583gr60)

[References        17](#h.redjrd46qo4b)

[Appendix        17](#h.jbzbvfsivok9)

* * *

Abstract
========

This project is to find torsion stiffness of the structure that is given in the project. All results ,methodologies and analyses are under Task1 , Task2 , Task3 and Task4 paragraphs. The results, rotationx= 0.0043 rad is acting on node 5 and 6 and 0.006m and -0.0129m displacements are acting on note 5 and 6. Which means that the vehicle twisted clockwise at 1.8328\*10^4 N. which is the total weight of the car including forces.

TS1 which is the initial torsion stiffness of a vehicle has 2~3 values. I concluded that Ts1 is 1.467\*10^4 Nm/deg

Introduction
============

This project is given the structure of a sedan frame.  The objective of this project is to find the torsion stiffness of this structure(see figure1) using the FEA method. All information about Length, thickness,side length, density , joints,coordinates and forces are in Appendix. Task1 is an initial model using only matlab.After initializing FEA model, divided model. Task 2 is to find Total weight of the car. Includes  forces. Task 3 and task 4 are to find Vehicle Torsion Stiffness

![](images/image38.png)

Figure.1 structure of sedan

Task 1. Initializing FEM model and dividing nodes
=================================================

Initializing fem model
----------------------

Coordinates were given in table.1. Nodes were connected Based on table.1, nodes connected and combined as elements then plotted(figure 2).

![](images/image34.png)

Figure.2: plotted after connected elements( number is refer to number of elements)

### Coding

Algorithm of plotting this structure is very simple.define number of elements using length or size. The looping process is Using while loop  number of elements times and using plot3(node x 1:2, nodes y 1:2, node z 1:2).

![](images/image19.png)

Figure.3: algorithm of plotting

 Dividing node processing
-------------------------

Diving nodes is very important in FEM. Because, usually more nodes have more accuracy. However, it will increase computing time and may result in inaccurate results due to code and program issues.

Dividing nodes instructure is below:

Each structural beam in Figure2 needs to be modeled by several finite element beam elements. The length of all middle beam elements for each beam structure should be 0.1 m. The length of the start and the end elements for each structural beam should be equal to each other and the maximum of their length should be 0.05 m.

What I understand is  new nodes that are close to original nodes are not over than 0.05m and between elements should not be over 0.1m(see figure 4).

![](images/image28.png)![](images/image17.png)

   Figure 4: example of dividing nodes

Divided nodes need L , m,n.l and d are required. L is the length of an element. m,n,l,D are the directions of cosines  xyz.  m,n,i,D will be the same as the original element. Because new nodes are under original elements. Codes for finding L,m,n,i,D explanations are under the appendix.

![](images/image25.png)

Figure 5: l,m,n

### Coding

Algorithms of the coding process can see figure 6. Which means that try to divide 0.1 first if there is any reminder then L\_n2divider will be reminder divide by 2. Then counts how many divide-able,  total divider is total elements going to add in elements.

![](images/image5.png)

Figure 6: algorithm of coding for dividing nodes process

After adding new nodes, we need to reconnect the original to new nodes.  the algorithm of the connecting process is figure 7.

![](images/image15.png)

Figure 7: algorithm of connect process

 The results
------------

After this the same algorithm is used for plotting. Result is in figure 8

![](images/image27.png)

Figure 8: result of divided nodes, each line of color is elements, blue circle is adjacent nodes.

Task 2. Weight and Load
=======================

Formula of weight is eq\[1\] . Total weight is  beams of weight + total force acting on the structure.And mass related to density and volume(eq\[2\]). Using eq\[1\] and eq\[2\] can be formed to eq\[3\].

weight=m\*9.81                                        \[1\]

m=p\*v                                                        \[2\]

weight =p\*v(1..n)\*9.81                                        \[3\]

Volume is Area multiplied by Length(eq\[4\]). Area is in eq\[5\]

V=A\*L                                                \[4\]

A=a^2-(a-2\*t)^2                                        \[5\]

Where:

a= side\_length

t= thickness

Side\_length and thickness of the beam is given in the instruction and figure 9 and figure 10.

![](images/image18.png)

Figure 9:thickness value in each elements

![](images/image20.png)

Figure 10:side length data each elements

Coding for finding volume and area is under the appendix.

### Coding

Density p=7850 kg/m^3 is given in the project manual.  

The results
-----------

I found that the total weight value is 18347N and 18328N for the divided one. difference between original and divided node about 0.22% and Total weight errors is 0.10%.  

Table1

| Metric           | Original Nodes | Divided Nodes | Error (%) |
|------------------|----------------|---------------|-----------|
| Structure Weight | 8546.7N        | 8527.5N       | 0.22%     |
| Total Weight     | 18347N         | 18328N        | 0.10%     |


Task 3.  Pure Torsion
=====================

Initial vehicle Torsion stiffness is how much the car is twisted by forcing acting on suspension.

It must be higher than suspension stiffness. If it is less than suspension stiffness, suspension will not function properly.  Calculate Ts = Initial Vehicle Torsion Stiffness needs a lot of information needed. But the basic formula is in eq\[6\]. In eq\[6\] , T is torque acting on node 5 and 6. T can be calculated F\*L

L is the length of width of the car F is the force that I sat on. T can also find total nodal forces acting in the Z direction of  node 5 or node 6 and multiply L/2. ![](images/image1.png) is the degree of torsion of structure. It can be calculated eq\[7\],d1z is the deformation of node 5 at z direction, d2z is the deformation of node 6 at z direction. Those can be found when the global matrix is set on.

![](images/image2.png)                                                \[6\]

![](images/image3.png)                                                \[7\]

To find the global matrix, we need to find thease Ix,Iy,Iz, K’, lambda, Transformation matrix, E,G,J. E and G are given in the project manual.calculate Ix,Iy,Iz,J can be found in the appendix. Algorithm is this figure 11.

![](images/image35.png)

Figure 11 : algorithm to find Ts1

Lambda
------

This equation in figure 12 can find the lambda

![](images/image6.png)![](images/image22.png)

Figure 12: lambda equation

L,l,m,n and D were calculated by matlab. Please see the appendix

There are two special condition of lambda

IF Z2>Z1

![](images/image10.png)

If Z2<Z1

![](images/image36.png)

Number of lambdas depends on the number of elements. Original nodes has 52 lambda, divided node has 630 lambdas

The results
-----------

This is lambda of element1 of original nodes

![](images/image26.png)

There are many lambdas, Please check my matlab file.

Transformation
--------------

Transformation matrix for 3D is a 12x12 matrix. Which can form figure 12.

![](images/image29.png)

Figure 12: transformation matrix equation

The results
-----------

In figure 13, this is result of Transformation matrix element 1 from original node

![](images/image32.png)

Figure 13. Transformation matrix from elemen1

K’
--

K’ means local stiffness matrix.  Equation can be found on figure 14.

![](images/image4.png)

Figure 14: 3d local stiffness matrix

The results
-----------

![](images/image16.png)

Global matrix
-------------

Global matrix is combine all together in one matrix with transformation(consider direction)

Which equation is this below figure 15.

![](images/image30.png)

Figure 15: equation of global matrix

The results
-----------

Result is a 3684x3684 matrix. Therefore, this figure 16 is just part of global matrix

![](images/image14.png)

Figure 16:part of global matrix for divided nodes

Initialize constrain and forces
-------------------------------

In the project manual, it mentioned that node 25 and 26 are constrained. Which means fully fixed

dx,dy,dz,mx,my,z=0. About adjacent nodes are already defined in figure 8 in task 1(see figure 17).

![](images/image12.png)

Figure 17: adjacent nodes,   blue dots at front are node 5 and 6

Adjacent nodes are \[261         291 503        255        270        296        260        531\].

Forces are defined in the manual see figure 18

![](images/image24.png)

Figure 18. Load that added in structure

When applied to forces into structure. Force will divide by the number of joints. Because forces are usually distributed equally. For Example, the front bumper has 200N with 2joints. The force act on each joint will be 100N. And all forces acting on Z direction.also total weight added on node 5 and 6

The results
-----------

Force and u(direction) will form a 3684x1 matrix. In figure19 is parts of results of force

![](images/image31.png)

Figure 19: part of forces

Displacement
------------

Displacement can be found using eq\[6\]

\[K\]^-1\*\[F\]=\[d\]                                                \[6\]

Where are:

K= global matrix

F= forces

d= displacement

The results
-----------

d(28) is mx for node 5 and d(35)is mx for node 6

d(28) =0.0043rad, d(35)=0.0043rad. Which means the front of the car is twisting clockwise.

![](images/image9.png)![](images/image39.png)

Then,  compared nodal forces. To confirm nodes are twisting.

![](images/image8.png)![](images/image23.png)

Figure 20: left is  local forces of element 7 and right is local forces of element 8(divided nodes)

Ts1
---

Initial Vehicle Torsion Stiffness unit is Nm/deg

Nm is momentum, Deg is rotation. I tried many different way to find Ts1

I used total nodal torsion moment zforce acting on node 5 and node 6 and divided by L

The results
-----------

Results Ts1= 1.6811\*10^6 Nm/rad and Ts1= 1.4672\*10^4 Nm/deg

![](images/image13.png)

First result is used normal formula eq\[6\] and eq\[7\]. Second one T is replaced to  total nodal z forces acting on node 5 or node 6 then multiply L/2. both result is similar therefore, TS1 is value is correct

The reason why Ts1 is -value is because,  control point is node 6 and it goes down.

Task 4 Torsion Study
====================

This will be similar to Task 3. However, Just forces will change 0 to total weight.

The results
-----------

Blue line is rotation of node 5, orange line is rotation of node6  both maximum output is 0.0043rad

![](images/image21.png)

Figure 21: torsion study of divided nodes

Rotation of Divided nodes has changed drastically, however rotation of original nodes has changed a little. Please check DATA in my matlab

![](images/image7.png)

        Figure 23: above is rotation of divided nodes. Down is rotation of original nodes

Discussion
==========

I found that matlab has some errors during this project. For example, my plot did not show in 3d unless I had to turn my plot to show 3d, sometimes values are changed, even though Original node code and divided node codes are almost identical.and local forces are similar to each other. It could be that the code was something wrong. However, I infer matlab has a problem. Also the computer could have issues because my computer starts crashing when testing a lot of times.

Another problem was divided nodes vs original nodes have value differences. Mass and volume were similar to each other, however,  stiffness and deformation were not similar. However, both help predict where structure is twisting to what direction. A divided node is more accurate than a not divided node.

Results
=======

Results can be checked above the task.  This structure has weightT = 1.8328\*10^4 N, rotationx= 0.0043 rad is acting on node 5 and 6 and 0.006m and -0.0129m displacements are acting on note 5 and 6. Ts1 is 1.467\*10^4 Nm/deg twisting clockwise rotation.

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

![](images/image33.png)

![](images/image11.png)