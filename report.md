# Report

![](https://github.com/TUDelft-MUDE/source-files/raw/main/file/1Ddynamic.png)

A building, considered as a rigid mass, is subject to an earthquake. The foundation of the building, interacting with the ground, is represented by a spring and a dashpot (damper).

The dynamic motion of the building is defined by the following differential equation:

$$ k \left(u_b(t)-u_g(t) \right) + c \left(\frac{d u_b}{d t} - v_g(t) \right) + m \left(\frac{d^2 u_b}{d t^2} \right) = 0 $$

where:
- $u_b$ = horizontal displacement of the building
- $u_g$ = horizontal displacement of the ground (= earthquake outcrop motion)
- $v_g$ = $du_g / dt$ = horizontal velocity of the ground
- $t$ = time
- $k$ = (shear) stiffness between the building foundation and the ground
- $c$ = damping between the building foundation and the ground
- $m$ = mass of the building

This is how the original earthquake data looks like:

![](https://github.com/TUDelft-MUDE/source-files/raw/main/file/Earthquake_data.png)

After having performed the tasks and computer exercises for this group assignment, you are requested to write a report by answering the following questions:

> **Question 1**
>
> Formulate the numerical expression for the acceleration $a_g(t)$ = $\frac{d v_g(t)}{d t}$ according to the Forward Difference scheme.


> **Question 2**
>
> Formulate the numerical expression for the displacement $u_g(t)$ = $\int{v_g(t) d t}$ according to the Trapezoidal Rule.


> **Question 3**
>
> Conclude on the accuracy of the calculated results from the comparison of your Python implementation with the original data (acceleration $a_g$ and displacement $u_g$). Explain possible differences.
>
> Were the results ($u_g$, $v_g$, $a_g$) according to your expectation?
> For example, comment on the values at the end of the recorded time series.


> **Question 4**
>
> Formulate the differential equation in a numerical scheme using the Central Difference scheme for the first and second derivative and by considering $u_b(t)$ = $u_b^i$ as the central point.
>
> Elaborate the numerical scheme such that the solution for the building displacement at the next time step $u_b(t + \Delta t)$ = $u_b^{i+1}$ is expressed explicitly in the other (known) >components.


> **Question 5**
>
> How many initial conditions are required to solve the differential equation?
>
> Formulate these initial conditions for the numerical scheme.


> **Question 6**
>
> Based on the variations of parameters k, c and m, what is the influence of individual parameters on the building response?
> 
> - What is the influence of the stiffness k on the solution?
> - What is the influence of the damping c on the solution?
> - What is the influence of the mass m on the solution?
> - If 'oscillations' occur, try explain their origin.
>


> By Ronald Brinkgreve and Anna Störiko, Delft University of Technology. CC BY 4.0, more info [on the Credits page of Workbook](https://mude.citg.tudelft.nl/workbook-2026/credits.html).

```{custom_download_link} ./all_files_GA_1_2.zip
:text: ".zip assignment"
:replace_default: "True"
```
