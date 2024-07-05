# Fourier Transform

Euler's formula demonstrates that if we were to take the exponential function of a complex number $e^{in}, n \in \mathbb{R}$ we would find ourselves on the point we would reach by walking counterclockwise $n$ units along a circle of radius 1 in the complex plane. This allows us to describe the process of rotating at a rate of $f$ cycles per second simply as $e^{2\pi ift}$, where $2\pi$ represents the full circumference of the circle, $f$ the desired frequency and $t$ is a variable for time. Therefore providing us a convenient notation for describing the winding of a circle. However, the convention for Fourier transforms is that the direction of movement is clockwise, rather than counterclockwise. Consequently, we will employ the following notation: $e^{-2\pi ift}$.

![[euler_formula_circle.png|300]]

Let us consider a general function, $g(t)$, and define the function $g(t)e^{-2\pi ift}$ as a function of time. This function will provide the value of $g$ at a given time, as well as the point along the circle. The next step is to determine a formula that can be used to capture the motion of the center of mass. One possible approach is to sample a large set of different times along the provided waveform, observe the resulting positions on the wound-up graph, and then take an average: $\frac{1}{N}\sum_1^N g(t)e^{-2\pi ift}$.

![[fourier_transform_center_mass.png]]

As the number of points included in the calculation increases, the resulting value becomes more precise. In the limit of an infinite number of points, the sum is equivalent to the integral: $\frac{1}{t_2-t_1}\int_{t_1}^{t^2} g(t)e^{-2\pi ift}$. The sole remaining distinction between this and the genuine Fourier transform is that the latter does not divide by the time interval; rather, it is simply the integral part $\int_{t_1}^{t^2} g(t)e^{-2\pi ift}$.

This implies that instead of focusing on the center of mass, it is necessary to scale it up by a certain amount. If the portion of the original graph that was being considered spanned three seconds, it would be necessary to multiply the center of mass by three. Similarly, if the portion spanned six seconds, it would be necessary to multiply the center of mass by six.

![[fourier_transform_center_mass_scaled.png]]

In physical terms, this has the effect that when a certain frequency persists for a long time, the magnitude of the Fourier transform at that frequency is scaled up more and more. To illustrate this, consider the image below, which shows a pure frequency of two beats per second being wound up at two cycles per second. Regardless of the duration of the signal, the centre of mass remains approximately constant. It is merely tracing the same shape.
![[fourier_transform_center_mass_corret_frequency.png]]
However, the genuine Fourier transform differs from our approximate Fourier transform in that the longer the signal persists, the greater the value of the Fourier transform at that frequency. For other winding frequencies, however, even those that are merely slightly different from 2, the effect of increasing the duration is negated by the fact that for longer time intervals, the wound-up graph is afforded a greater opportunity to achieve equilibrium around the circle.
![[fourier_transform_center_mass_wrong_frequency.png]]