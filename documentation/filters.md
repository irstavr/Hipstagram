# TECHNICAL DOCUMENTATION

## Interface: filters scripts

For the part of image processing and filter implementation, we based on an already tested and 
developed filter (‘retro’ - link is given on ‘resources’ page) and based on the technique of that 
filter we implemented all the following instagram-like filters:
● Gotham (corresponds to our ‘blacknwhite’)
● Lomo-fi (corresponds to our ‘adjcontrast’) 
● Lily   (corresponds to our ‘sepia’)
● Walden (corresponds to our ‘holga’)
As an extra filter we implemented the ‘artistica’ filter in order to differ from the classic instagram filters.

### For the implementation:
Some  filters have 5 parameters used to manipulate colors, contrasts etc
● alpha - weight for yellow tone
● beta  - weight for desaturation
● gamma - weight for blue adjustment
● delta - weight for burning the edges of the image
● epsilon - used to normalize perturbations.

### Retro filter

This filter is the example filter. In this filter there is variable saving the average of image’s 
channels and multiply with weight for blue to make images colors more delicately
    `(img(:,:,3) = (1-gamma)*img(:,:,3) + gamma*i)`
Then the image have to desaturate (decrease the values of pixels on each channel).
Last step is to make the edges darker..

### Blacknwhite filter
This filter converts the original image’s colors to black and white and adds a black frame.
All of the parameters above are near to 0.The black frame is nihilism of several image’s pixel.For 
example with this command `img(1:end,1:15,:) = 0;` it is created the left part of frame 
respectively are created the other frame’s parts.
The differences from retro filter are the changes on weights and the addendum of the frame.

### Sepia filter
This filter gives a sense of yellow tone. We have to increase the weight for yellon tone to convert 

### Hipstagram  6
the original image to an image which main color is yellow.
The value of parameter alpha is the difference between sepia filter and retro.

### Holga filter
This filter keeps the blue and green  iimage’s channels.To keep blue and green  color we have to 
make the red channel of the image 0. 
    ( img(:,:,1)=0; )
In this filter we don’t use parameters referred bellow. From example filter(retro filter) we used 
only the technique for making darker the edges. 

### Artistica filter
This filter gives a sense of an old image.We adjust the values of parameters alpha,beta, gamma, 
delta, epsilon in such way to make the image more “noisy”. For example, the value of 
epsilon is 0,5 in contrast to retro filter .As we increase  this parameter more noise is created on 
the image.
The difference between artistica filter and retro is the values of parameters 
alpha,beta,gamma,delta,epsilon.
 
### Adjcontrast  filter
In this filter we used a function called sigmoid.The sigmoid function has the characteristics that 
it is a smooth continuous function, the function outputs within the range -1 to 1.The sigmoid is 
mathematical type `f(t)=1/1+e^(-t)`.To adjust image’s contrast we have to modify this function and 
instead of e we used a variable called gain.Gain is the parameter that regulates the contrast.So 
sigmoid function in our code seem like this  `newim =  1./(1 + exp(gain*(cutoff-newim)))`.
This filter doesn’t have similarities with retro filter.
