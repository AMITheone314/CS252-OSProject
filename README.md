# 4.22 Writing a Multi-Threaded Program

Write a multithreaded program that calculates various statistical values
for a list of numbers. This program will be passed a series of numbers
on the command line and will then create three separateworker threads.
One thread will determine the average of the numbers, the second will
determine the maximum value, and the third will determine the minimum
value. 

For example, suppose your program is passed the integers
90 81 78 95 79 72 85

>The program will report<br>
>The average value is 82<br>
>The minimum value is 72<br>
>The maximum value is 95<br>

The variables representing the average, minimum, and maximum values
will be stored globally. The worker threads will set these values, and
the parent thread will output the values once the workers have exited.
(We could obviously expand this program by creating additional threads
that determine other statistical values, such as median and standard
deviation.)
