# Cycloid Series

This is a SageMath script that graphs a cycloid using a Fourier Series representation:
<img src="Cycloid.svg?raw=true">

## Raw:

Here is the raw text, for those not working in a Jupyter notebook:

```sage
# This is a really neat Fourier Series that is equivalent to a cycloid. This is fascinating 
#  due to the way the change of variables happens for the coefficients in the series. That is, 
#  a cycloid has no implicitization, only a parametric representation, so a change of 
#  variables must happen within the Fourier coefficients to obtain this series.
#
# Author: Luke V.

# resolution of sum
r = 100

x = var('x')
t = var('t')

# cycloid and first derivative of x
fx = t - sin(t)
fy = 1 - cos(t)
diffx = diff(fx, t)

# find the root so we can chage the bounds of our integrals
lim = find_root(fx == 2 * pi, 0, 2 * pi)

# atrocious fourier series
func = 1 / (2 * pi) * (1 / 2 * (numerical_integral(fy * diffx, -lim, lim)[0])
                        + sum(
                        (numerical_integral(fy * diffx * cos(n * pi * (fx) / lim), -lim, lim)[0]) * cos(n * x / 2)
                        for n in xrange(2, r, 2))) # every odd term is zero, skip calculating them

# plot the series and the first arch of the cycloid
p = plot(func, (x, -4 * pi, 4 * pi), aspect_ratio=1, color='blue')
p1 = parametric_plot((fx, fy), (t, 0, 2 * pi), aspect_ratio=1, color='red')

# show the series with the first arch of the cycloid drawn on top
show(p + p1)
```
