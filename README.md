#Ion Experiment 11

These data are collected with variable flow rates at a 0.5 inch standoff with a fuel/oxygen ratio of 0.82.  These tests are to provide validating experimental data for a parallel computational model developed at Virginia Tech.

In these experiments, data were collected using the same custom amplifier used in previous tests.  It is a two-channel precision circuit that can command either voltage or current in response to an excitation provided by the T7 DAQ.

## cal.dat
`cal.dat` was collected with no flame.  Instead, a constant 10V (approx) excitation was applied to the torch, and a precision 10uA shunt was manually engaged and released during the test.  In this way, the current measurement calibration was verified.  The signal was relatively noisy (about +/-1uA) since the connection was made with a substantial unshielded loop.

## NN.dat
Data files `10.dat` through `25.dat` include IV characteristics for nominal flow rates 10scfh through 25scfh, all with F/O ratio 0.82.  The actual measured flow rates (using thermal mass flow meters) for methane and oxygen are recorded as "meta" parameters in the header of each file.

The raw data for each channel is recorded in voltage.  For the torch voltage (the second channel configured), this is correct as-is, and does not need to be calibrated.  For the current signal (the first channel configured), the signal should have a slope and offset applied as specified in the header.  The slope is in units uA/V, and the offset is specified in the form of the "zero" voltage, so the current can be caculated 
```
I = aicalslope * (V - aicalzero)
```

## Noise
There appears to be a persistent 1uA noise in the signal.  It is possible to achieve cleaner signals, but the source of the noise in this test is not yet entirely clear.  The data are sufficiently dense and sufficiently self-consistent, that grouping the data into voltage bins and averaging the current in each should be an acceptable means of filtering the data in post-processing.

## Using Python
The `lconfig.py` module included with this dataset automatically applies the appropriate calibration in Python.  If you are using Python to perform analysis, you can get started with
```python
import lconfig as lc
c = lc.LConf('filename.dat', data=True, cal=True)
c.show_channel(0)
lc.plt.show()	# may not be necessary; depends on Matplotlib config
```

