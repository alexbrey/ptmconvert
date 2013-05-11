ptmconvert
==========

A command-line tool to create false-color images of the normals in an RTI/PTM file.

Introduction
----------------

This is a program created by Tobias Alexander Franke, which I have simply moved to github from his google code page. I do not claim to have created any part of it. You can learn more about Mr. Franke's PTM research here: http://www.tobias-franke.eu/projects/ptm/

Polynomial Texture Maps are special texture files which contain biquadratic polynomial coefficients per pixel, modeling the reflectance behavior under varying incident radiance. Even though the format is in heavy use in archeology, I found that the available open-source implementations are rather sparse. The following code is a one-file C++ converter which reads (at the moment) LRGB encoded PTMs (either uncompressed or with JPEG compression) and dumps the luminance coefficients and the RGB data into separate PNG images. These images can be used without the need to write a PTM reader for instance in web applications using WebGL. The neccessary scale and bias parameters are printed on the console.

If you're looking for a simple reader converting all data into regular char arrays, look no further! The code should be simple enough to parse, just have a look at ptm_dump on how to get to the data. A big Thank You! to Sean Barrett for stb_image, which I use to read JPEG compressed data and write PNG files to the disk.

Luminance based PTMs contain 9 values per pixel, 6 luminance coefficients for the polynomial and 3 color values. These are converted into three separate images:

a regular RGB image for colors
an image with coefficients 1, 2 and 3 saved as RGB
an image with coefficients 4, 5 and 6 saved as RGB
Together with the bias and scale values, one can use these images with a shader and reconstruct the PTM without the need for a PTM loader.


Setup
----------

To compile ptmconverter you must first use CMake to create a makefile, and then run make. CMake can be downloaded here: http://www.cmake.org/

To run ptmconverter, type ./ptmconvert followed by the name of your ptm file, for example:
./ptmconvert myPTMfile.ptm