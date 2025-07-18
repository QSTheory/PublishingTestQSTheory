
Adding Coordinate Grids to the FFT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The continuous Fourier transform is defined as:

.. math::


   \begin{aligned}
       \mathcal{F}&: \ G(f) = \int_{-\infty}^{\infty}dx \ g(x)\ e^{- 2 \pi i fx},\quad \forall\ f\in \mathbb R,\\
       \widehat{\mathcal{F}}&: \ g(x) = \int_{-\infty}^{\infty}df\ G(f)\ e^{2 \pi i fx},\quad \forall\ x \in \mathbb R.
   \end{aligned}

When discretizing it on a finite grid in position and frequency space,
one does not only get the Fast Fourier transform (FFT) but some
additional phase and scale factors:

.. math::


   \begin{aligned}
       x_n &\coloneqq x_\mathrm{min} + n  \Delta x, \quad n = 0, \ldots, N-1 ,\\
       \quad f_m &:= f_\mathrm{min} + m \Delta f, \quad m = 0, \ldots, N-1,
   \end{aligned}

.. math::


   \begin{aligned}
       \text{(gdFT)} \quad G_m
       &= \Delta x \ \sum_{n=0}^{N-1} g_n \ \exp \left({-2 \pi i \ \left( f_\mathrm{min} + m \Delta f \right) \left( x_\mathrm{min} + n \Delta x \right) }\right) \\
       &= \Delta x
           \ {\textcolor{green}{\exp \left({\textcolor{green}{-} 2\pi i \ x_\mathrm{min} \  m \Delta f}\right)}}
           \ {\textcolor{green}{\exp \left({\textcolor{green}{-} 2\pi i \ x_\mathrm{min} \ f_\mathrm{min}}\right)}}
           \ \ \textcolor{black}{\mathrm{fft}} \left(
               g_n \ {\textcolor{green}{\exp \left({\textcolor{green}{-} 2\pi i \ f_\mathrm{min} \ n \Delta x}\right)}}
           \right),
   \end{aligned}

.. math::


   \begin{aligned}
       \text{(gdIFT)} \quad g_n
       &= \Delta f \ \sum_{m=0}^{N-1} G_m \ \exp  \left({2 \pi i \ \left( f_\mathrm{min} + m \Delta f \right) \left( x_\mathrm{min} + n \Delta x \right) } \right) \\
       &= {\textcolor{green}{\exp \left({\textcolor{green}{+} 2\pi i \ f_\mathrm{min} \ n \Delta x}\right)}}
           \ \ \textcolor{black}{\mathrm{ifft}} \left(
               G_m \ {\textcolor{green}{\exp \left({\textcolor{green}{+} 2\pi i \ x_\mathrm{min} \  m \Delta f}\right)}}
               \ {\textcolor{green}{\exp \left({\textcolor{green}{+} 2\pi i \ x_\mathrm{min} \ f_\mathrm{min}}\right)}} / \Delta x
           \right).
   \end{aligned}

:math:`\mathrm{fft}` and :math:`\mathrm{ifft}` follow here the
definition of NumPy’s default behavior in its `Discrete Fourier
Transform <https://numpy.org/doc/stable/reference/routines.fft.html>`__
module.
