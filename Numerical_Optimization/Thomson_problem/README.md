# Thomson problem

The objective of the **Thomson problem** is to determine the minimum **electrostatic potential energy** configure of N electrons constrained to the surface of a unit sphere that repel each other with a force given by **Coulomb's law**.

The electrostatic interaction energy:
$$
U_{ij}(N)=k_e \frac{e_{i}e_j}{r_{ij}}
$$
Simplified units of $e=1$ and $k_e=1$ are used without loss of generality. Then
$$
U_{ij}(N)=\frac{1}{r_{ij}}
$$
The total electrostatic potential energy of each N-electron configure may then be expressed as the sum of all pair-wise interactions
$$
U(N)=\sum_{i<j}\frac{1}{r_{ij}}
$$
The global minimization of $U(N)$ over all possible of N distinct points is typically found by numerical minimization algorithms.

## Pseudo code





## Configurations of n=100 points

* Initial random configuration

![](https://github.com/edj19/Algorithms/blob/master/Numerical_Optimization/Thomson_problem/figures/sphere.jpg)



* equilibration configuration

![](https://github.com/edj19/Algorithms/blob/master/Numerical_Optimization/Thomson_problem/figures/sphere_init.jpg)

















