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

##Solution

Global Variables: As mentioned in the question we have to globally define average, minimum, and maximum values

/*  The Average, Minimum, Maximum Values: */
float average;
float minimum;
float maximum;
The other global variables

/*  Global Variables    */
#define MAX_COUNT 500000
float array[MAX_COUNT];
int element_count;
long long int i;
int worker_threads[3];
MAX_COUNT is the maximum size of array. element_count is the number of elements user wants to enter. i is the common looping variable globalized for convienience. worker_threads[3] is an array storing the returned values of pthread_create()

Input function:

/*  Input Function  */
void input()
{
    printf("Enter element count: ");
    scanf("%d",&element_count);
    for(i=0;i<element_count;i++)
    {
        scanf("%f",&array[i]);
    }
}
We define 3 functions for start_routine namely thread_average, thread_minimum, thread_maximum as below:

void *thread_average()
{
    float sum=0;
    for(i=0;i<element_count;i++)
    {
        sum  = sum + array[i];
    }
    average = sum / element_count ;
    printf("\nThe average value is %f",average);
}
void *thread_minimum()
{
    float temp;
    temp = array[0];
    for(i=0;i<element_count;i++)
    {
        if(array[i]<temp)
        {
            temp = array[i];
        }
    }
    minimum = temp;
    printf("\nThe minimum value is %f",minimum);
}
void *thread_maximum()
{
    float temp;
    temp = array[0];
    for(i=0;i<element_count;i++)
    {
        if(array[i]>temp)
        {
            temp = array[i];
        }
    }
    maximum = temp;
    printf("\nThe maximum value is %f",maximum);
}
