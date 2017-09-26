About
-----

Python Module for manipulating SMPTE timecode. Supports 23.98, 24, 25, 29.97,
30, 50, 59.94, 60 frame rates and milliseconds (1000 fps).

This library is a fork of the original PyTimeCode python library. You should
not use the two library together (PyTimeCode is not maintained and has known
bugs).

The math behind the drop frame calculation is based on the
[blog post of David Heidelberger](http://www.davidheidelberger.com/blog/?p=29).

Simple math operations like, addition, subtraction, multiplication or division
with an integer value or with a timecode is possible. Math operations between
timecodes with different frame rates are supported. So:

    from timecode import Timecode
  
    tc1 = Timecode('29.97', '00:00:00:01')
    tc2 = Timecode('24', '00:00:00:10')
    tc3 = tc1 + tc2
    assert tc3.framerate == '29.97'
    assert tc3.frames == 11
    assert tc3 == '00:00:00:11'

Creating a Timecode instance with a start timecode of '00:00:00:00' will
result a timecode object where the total number of frames is 0. So:

    tc4 = Timecode('24', '00:00:00:00')
    assert tc4.frames == 0

Use the ``frame_number`` attribute if you want to get a 1 based frame number:

    assert tc4.frame_number == 1

Frame rates 29.97 and 59.94 are always drop frame, and all the others are non
drop frame.

The SMPTE standard limits the timecode to 24 hours. All maths performed by
Timecode is therefore performed modulo ``one_day``.

Please report any bugs to the [GitHub](https://github.com/Nick-Shaw/timecode)
page.

Original Copyright 2014 Joshua Banton and PyTimeCode developers.
This version Copyright 2017 Nick Shaw, Antler Post
