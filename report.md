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


**Solution**

Forward Difference scheme:

$$ a_g(t) = \frac{v_g(t+\Delta t) - v_g(t)}{\Delta t} $$

or

$$ a_g^i = \frac{v_g^{i+1} - v_g^i}{\Delta t} $$


> **Question 2**
>
> Formulate the numerical expression for the displacement $u_g(t)$ = $\int{v_g(t) d t}$ according to the Trapezoidal Rule.


**Solution**

Trapezoidal Rule:

$$ u_g(t + \Delta t) = u_g(t) + \frac{\Delta t}{2} \left[v_g(t+\Delta t) + v_g(t) \right] $$

or

$$ u_g^{i+1} = u_g^i + \frac{\Delta t}{2} \left(v_g^{i+1} + v_g^i \right) $$

> **General feedback**
> 
> Many groups have used summation over all steps of velocity $v_g$ without adding the displacement from the previous step ($u_g^i$) or the initial displacement ($u_g^0$). This is incorrect.


> **Question 3**
>
> Conclude on the accuracy of the calculated results from the comparison of your Python implementation with the original data (acceleration $a_g$ and displacement $u_g$). Explain possible differences.
>
> Were the results ($u_g$, $v_g$, $a_g$) according to your expectation?
> For example, comment on the values at the end of the recorded time series.


**Solution**

Calculated results are visually the same as the original data, which means: they seem accurate.

Acceleration and velocity are expected to be zero at the end of the recorded time series. Indeed, they seem to be very small.

Displacement at the end of the time series is not zero. This may be due to the following causes:

1. The ground surface may have moved permanently as a result of the earthquake.
2. The earthquake record was originally based on measured discrete accelerations, and was not corrected for drift (= final displacement resulting from the double numerical integration of the discrete acceleration data, rather than a physically measured displacement).

> **General feedback**
>
> It was essential to comment on the displacement, velocity, and acceleration at the end of the time series. Specifically, the velocity and acceleration go to zero (no more motion), but the displacement does not (indicating permanent ground deformation). You were not expected to calculate the accuracy quantitatively.


> **Question 4**
>
> Formulate the differential equation in a numerical scheme using the Central Difference scheme for the first and second derivative and by considering $u_b(t)$ = $u_b^i$ as the central point.
>
> Elaborate the numerical scheme such that the solution for the building displacement at the next time step $u_b(t + \Delta t)$ = $u_b^{i+1}$ is expressed explicitly in the other (known) >components.


**Solution**

$$ k u_b^i + c \frac{u_b^{i+1} - u_b^{i-1}}{2 \Delta t} + m \frac{u_b^{i+1} - 2 u_b^i + u_b^{i-1}}{\Delta t^2} = k u_g^i + c v_g^i $$

$$  \left( \frac{c}{2 \Delta t} + \frac{m}{\Delta t^2} \right) u_b^{i+1} = \left( -k + \frac{2 m}{\Delta t^2} \right) u_b^i + \left( \frac{c}{2 \Delta t} - \frac{m}{\Delta t^2} \right) u_b^{i-1} + k u_g^i + c v_g^i $$

$$ u_b^{i+1} = \left[ \left( -k + \frac{2 m}{\Delta t^2} \right) u_b^i + \left( \frac{c}{2 \Delta t} - \frac{m}{\Delta t^2} \right) u_b^{i-1} + k u_g^i + c v_g^i \right] / \left( \frac{c}{2 \Delta t} + \frac{m}{\Delta t^2} \right) $$


> **Question 5**
>
> How many initial conditions are required to solve the differential equation?
>
> Formulate these initial conditions for the numerical scheme.


**Solution**

Since the differential equation is second order, $two$ initial conditions are required:

1. Initial building displacement is zero
2. Initial building velocity is zero

$$ u_b^0 = 0 $$

and

$$  v_b^0 \approx \frac{u_b^1 - u_b^0} {\Delta t} = 0; u_b^1 = u_b^0 = 0 $$

> **General feedback**
>
> You must elaborate the $v_b = 0$ condition in terms of displacement using forward difference method because our numerical scheme is in terms of $u_b$ so the initial conditions must also be in same terms. Thus, the two conditions are: $u_b^0=0$ , $u_b^1=0$.


> **Question 6**
>
> Based on the variations of parameters k, c and m, what is the influence of individual parameters on the building response?
> 
> - What is the influence of the stiffness k on the solution?
> - What is the influence of the damping c on the solution?
> - What is the influence of the mass m on the solution?
> - If 'oscillations' occur, try explain their origin.
>


**Solution**

- Higher stiffness makes the building following the ground motion more closely. It also causes higher vibration/oscillation frequencies.
- Higher damping also makes the building follow the ground motion more closely. It also damps out vibrations/oscillations more.
- Higher mass makes the building following the ground motion more slowly. It also causes lower vibration/oscillation frequencies.

(For all cases where k = c = m, the solution is (approximately) the same, irrespective of the actual values).
 
Oscillations that might be observed with some parameter combinations could, in general, have a physical or numerical origin:

- Physical: If the earthquake signal approximates the eigenfrequency of the system (based on the specific combination of parameters), oscillations could be a result of resonance.
- Numerical: If the time step is too large, oscillations could be a result of numerical instability (when using a Forward Difference scheme). This will be discussed in more detail in Week 1.3.

> **General feedback**
>
> Oscillations originate due to resonance (when the earthquake matches the eigen frequency roughly). Many groups focus on the damping (underdamped systems) and stiffness which explains the nature of oscillations (amplitude and delay) but are not the "origin". 


> By Ronald Brinkgreve and Anna Störiko, Delft University of Technology. CC BY 4.0, more info [on the Credits page of Workbook](https://mude.citg.tudelft.nl/workbook-2026/credits.html).

```{custom_download_link} ./all_files_GA_1_2.zip
:text: ".zip assignment"
:replace_default: "True"
```
