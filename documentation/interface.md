# Interface: C script

Script files of .c code are mainly used for the implementation of the interface between GIMP and 
Octave, on how these two programs can co-operate and produce the new filtered image.
 
The technique that is used in order to apply filters on Gimp by using Octave to run the filters 
code is the following:
Gimp loads the image that is opened in its interface. 
From the function `octave_region()` of every `.c` file, the (opened) image on GIMP is read and 
written in a new file with the name “MatrixIn.txt1” with the values of its color elements.

    matrixIn = fopen( octave_params.cinput, "w" );
    fprintf ( matrixIn, "%i\n", (gint)layerIn[coord( i, j, k, bpp, width )]);

On the second phase, Octave is called by a system call to run:
    
    char command[PATH_MAX + 1];
    strcpy ( command, "octave --silent " );
    strcat ( command, octave_params.cscript );
    ret = system ( command );

Octave is running the file `<filter_name>.m` and reads the file “MatrixIn.txt”.
It follows the image processing code and at the end it saves the new edited with hipstagram filter 
image in a new file, named “MatrixOut.txt”
Octave closes and we return back to `octave_region()` function which on the next step,
will perform the second interface of GIMP and Octave as it sends back the “MatrixOut.txt” to 
GIMP in order to depict the new image.
             
    matrixOut = fopen (octave_params.coutput, "r" );

Then, GIMP is ready to show us the new image on its panel.
