# Advanced Lighting
## A rough table of content
1. The rendering equation
   1. Whats all the fuzz?
   2. How does it work?
   3. Limitations
2. BRDF
   1. Introduction in BRDF
3. Physically based BRDF (Cook torrance)
4. Global Illumination
   1. Image based lighting
   2. Other methods
5. Further advanced rendering and lighting methods

## The Rendering Equation
To synthesise a image from a virtual 3D scene we need a way to describe and calculate how light behaves and interacts with the objects in our scene. Often times it is desirable to produce photorealistic images which means we can use physical observations to base our model on. Kajiya James wrote a paper 1986 titled 'The rendering equation' in which he generalized a variety of older rendering techniques. The equation he came up with is regarded as the best model there is for simulating the behaviour of light. Most rendering algorithms can be considered as approximating his equation more or less accuratly.

This is the equation as presented on wikipedia:
<p align="center">
  <img src="https://latex.codecogs.com/gif.latex?L_{\text{o}}(\mathbf&space;x,&space;\omega_{\text{o}},&space;\lambda,&space;t)&space;=&space;L_e(\mathbf&space;x,&space;\omega_{\text{o}},&space;\lambda,&space;t)&space;&plus;&space;\int_\Omega&space;f_r(\mathbf&space;x,&space;\omega_{\text{i}},&space;\omega_{\text{o}},&space;\lambda,&space;t)&space;L_{\text{i}}(\mathbf&space;x,&space;\omega_{\text{i}},&space;\lambda,&space;t)&space;(\omega_{\text{i}}\cdot\mathbf&space;n)&space;\operatorname&space;d&space;\omega_{\text{i}}" alt="The rendering equation"/>
</p>

### Simplifying the Rendering Equation

Most of the time using a simplified version of it is sufficient. The wavelength (![lamda](https://latex.codecogs.com/gif.latex?\lambda)) can usually be ignored because we often use a RGB triple to describe the wavelength of a light source. Also our current screens are only able to emit light in these three wavelength. We basically solve the rendering equations three times for each wavelength instead of using a complete wavelength-spectrum of a 'realistic' lightsource.

![time](https://latex.codecogs.com/gif.latex?t) allows us to calculate the radiance for a specific time ![time](https://latex.codecogs.com/gif.latex?t). We don't need it if we keep the 'power output' of a lightsource constant or evaluate the 'power output' beforehand. (i. e. before trying to solve the equation).


The part ![light emition](https://latex.codecogs.com/gif.latex?L_e(\mathbf&space;x,&space;\omega_{\text{o}},&space;\lambda,&space;t)) is the emitted radiance of point ![x](https://latex.codecogs.com/gif.latex?x). Since most objects dont emit light themselfs this is more often than not 0.

These sipmlifications leave us with the following equation sometimes denoted as the reflectance equation:


<p align="center">
   <img src="https://latex.codecogs.com/gif.latex?L_o(x,\omega_o)&space;=&space;\int\limits_{\Omega}&space;f_r(x,\omega_i,\omega_o)&space;L_i(x,\omega_i)(&space;n&space;\cdot&space;\omega_i)&space;d\omega_i" alt="The reflectance equation"/>
</p>
