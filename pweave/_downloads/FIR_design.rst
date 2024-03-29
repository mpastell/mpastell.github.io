=========================================
 FIR filter design with Python and SciPy
=========================================

:Author: Matti Pastell <matti.pastell@helsinki.fi>
:Website: http://mpastell.com
:Date: May 20th 2013



Introduction
============

This an example of a document that can be published using `Pweave
<http://mpastell.com/pweave>`__. Text is written using
reStructuredText and code between `<<>>` and `@` is
executed and results are included in the resulting document.

You can define various options for code chunks to control code
execution and formatting (see `FIR design with
SciPy <http://mpastell.com/2010/01/18/fir-with-scipy/>`__
).

FIR Filter Design
=================

We'll implement lowpass, highpass and ' bandpass FIR filters. If you
want to read more about DSP I highly recommend `The Scientist and
Engineer's Guide to Digital Signal
Processing <http://www.dspguide.com/>`__ which is freely available
online.

Functions for frequency, phase, impulse and step response
---------------------------------------------------------

Let's first define functions to plot filter properties.



.. code:: python

    from pylab import *
    import scipy.signal as signal
        
    #Plot frequency and phase response
    def mfreqz(b,a=1):
        w,h = signal.freqz(b,a)
        h_dB = 20 * log10 (abs(h))
        subplot(211)
        plot(w/max(w),h_dB)
        ylim(-150, 5)
        ylabel('Magnitude (db)')
        xlabel(r'Normalized Frequency (x$\pi$rad/sample)')
        title(r'Frequency response')
        subplot(212)
        h_Phase = unwrap(arctan2(imag(h),real(h)))
        plot(w/max(w),h_Phase)
        ylabel('Phase (radians)')
        xlabel(r'Normalized Frequency (x$\pi$rad/sample)')
        title(r'Phase response')
        subplots_adjust(hspace=0.5)
    
    #Plot step and impulse response
    def impz(b,a=1):
        l = len(b)
        impulse = repeat(0.,l); impulse[0] =1.
        x = arange(0,l)
        response = signal.lfilter(b,a,impulse)
        subplot(211)
        stem(x, response)
        ylabel('Amplitude')
        xlabel(r'n (samples)')
        title(r'Impulse response')
        subplot(212)
        step = cumsum(response)
        stem(x, step)
        ylabel('Amplitude')
        xlabel(r'n (samples)')
        title(r'Step response')
        subplots_adjust(hspace=0.5)




Lowpass FIR filter
------------------

Designing a lowpass FIR filter is very simple to do with SciPy, all you
need to do is to define the window length, cut off frequency and the
window.

The Hamming window is defined as:
:math:`w(n) = \alpha - \beta\cos\frac{2\pi n}{N-1}`, where
:math:`\alpha=0.54` and :math:`\beta=0.46`

The next code chunk is executed in term mode, see the `source document
<FIR_design.rstw>`_ for syntax. Notice also that Pweave can now catch
multiple figures/code chunk.



.. code:: python

    n = 61
    a = signal.firwin(n, cutoff = 0.3, window = "hamming")
    #Frequency and phase response
    mfreqz(a)


.. image:: figures/FIR_design_figure2_1.png
   :width: 15 cm


.. code:: python

    show()
    #Impulse and step response
    figure(2)


.. code::

    <matplotlib.figure.Figure at 0x7f83f3f52b00>
    

.. code::

    <matplotlib.figure.Figure at 0x7f83f3f52b00>
    


.. code:: python

    impz(a)


.. image:: figures/FIR_design_figure2_1.png
   :width: 15 cm


.. code:: python

    show()
    




Highpass FIR Filter
-------------------

Let's define a highpass FIR filter:



.. code:: python

    n = 101
    a = signal.firwin(n, cutoff = 0.3, window = "hanning", pass_zero=False)
    mfreqz(a)
    show()


.. image:: figures/FIR_design_figure3_1.png
   :width: 15 cm



Bandpass FIR filter
-------------------

Notice that the plot has a caption defined in code chunk options.



.. code:: python

    n = 1001
    a = signal.firwin(n, cutoff = [0.2, 0.5], window = 'blackmanharris', pass_zero = False)
    mfreqz(a)
    show()


.. figure:: figures/FIR_design_figure4_1.png
   :width: 15 cm

   Bandpass FIR filter.


