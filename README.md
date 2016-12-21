# Segmentation of moth and butterfly images

This repository collects a few tools to segment and analyze moth images
with canonical poses. With standard and very simple segmentation
techniques, we are able to perform a large-scale quantification of a
huge dataset estimating sizes and color information. Furthermore, we can
process images with a small calibration pattern to allow for estimating absolute
measures.

Author: _Erik Rodner_ (Computer Vision Group, Friedrich Schiller
University of Jena)

## What you need to use this software

1. Python 2.7
2. numpy, scipy
3. matplotlib/pylab for visualization
4. skimage for image processing
5. Other common python packages, such as json etc.
6. Linux or MacOS; the program should also run on Windows with minor
   modifications

## Segmentation and quantification

The main tool for segmentation is ``seg.py``. If you have everything
installed and want to run a first test, simply call the program as
follows from your command line:
```bash
python seg.py test.jpg
```
which should output the following on the terminal
```
1/1 test.jpg: (1024, 683)
Threshold: 0.201171875
Calibration length bounds: 11.0 <= d <= 25.8
Statistics in segmented region: {
  "height-calibrated": 38.492167681756925, 
  "calibration-length": 12.5, 
  "mean-v": 0.30125312140978533, 
  "c-xmin": 79.718389423076928, 
  "median-v": 0.25882352941176473, 
  "c-length": 7839, 
  "stddev-v": 0.16121264171588823, 
  "absolute-size": 175535, 
  "relative-size": 0.2509822817532943, 
  "c-xmax": 944.6045903344849, 
  "c-ymin": 94.471512957317074, 
  "c-area": 199125.72196888566, 
  "c-area-calibrated": 1274.4046206008682, 
  "c-ymax": 575.62360897927863, 
  "width-calibrated": 69.190896072912636
}
```
and in addition show the following on the screen:
![alt text](https://github.com/erodner/mothseg/blob/master/doc/screenshot.png "Screenshot of a demo result")

You can specify multiple images on the command line if you want to perform processing for the entire dataset.
In this case, I recommend to use:
```
python seg.py --displaymode pdf --outstats results.json test1.jpg test2.jpg ...
```
to write out the results as text to ``results.json`` (in JSON format) and as images to several pdf files.
Furthermore, the segmentation can be controlled with some parameters for adjusting it to your images, please see ``python seg.py -h`` for details.

## Further notes

1. The calibration can fail for which in this case the respective variables ``c-area-calibrated``, ``height-calibrated``, and ``width-calibrated`` are
not available in the results.
2. The segmentation and calibration pattern detection is simple and might need some additional thoughts for more difficult datasets.
3. If the segmentation fails, try to adjust the alpha parameter by ``--alpha 0.8`` or something similar. Good luck :)

## Disclaimer

This work has been created as part of a cooperation project at the University of Jena. The images have been provided by Gunnar Brehm.
