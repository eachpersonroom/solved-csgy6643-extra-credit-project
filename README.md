Download Link: https://assignmentchef.com/product/solved-csgy6643-extra-credit-project
<br>
<ol>

 <li><strong>A) Optical Flow </strong></li>

</ol>

In this project, you will implement the <u>Lucas-Kanade</u> and <u>Horn-Schunck</u> optical flow methods. Both methods are based on spatial and temporal derivatives, differing mainly in the optimization approach.

<strong>Implementation: </strong>




<ol>

 <li>Assume <u>two</u> images with the same dimensions, e.g. im1 = sphere0.png and im2 = sphere1.png.</li>

 <li>Compute <u>spatial partial derivative images <strong><em>I<sub>x</sub></em></strong> and <strong><em>I<sub>y</sub></em></strong> for im1</u> using any method of your choice.</li>

</ol>

<ol start="3">

 <li>Compute temporal partial derivative <strong><em>I<sub>t</sub></em></strong>. This can be approximated by image difference im2 – im1.</li>

</ol>

<strong>Implement Lucas-Kanade </strong>

This method solves for optical flow by assuming constant flow within a neighborhood (patch), centered around the current pixel (<em>i,j)</em>. Using this assumption, a linear system is constructed and solved to find u<sub>i,j</sub> and v<sub>i,j</sub>. This means you must repeat this process for every pixel in the image.

Consider using a neighborhood size of 5×5. This results in the linear system shown below, with a matrix consisting of spatial partial derivatives and a vector of temporal partial derivatives at all points in the neighborhood p<sub>i</sub>. Solve this system of equations via linear least squares to find u<sub>i,j</sub> and v<sub>i,j</sub>.

<u>Note, this is not the value of u and v for the entire neighborhood, only for the pixel <em>(i,j). </em>Repeat this process for</u> <u>every pixel in the image.</u> You may ignore the boundary of the image where you cannot sample a full neighborhood.

<strong>Implement Horn-Schunck </strong>

<strong> </strong>

This method solves for optical flow by imposing a smoothness penalty on the optical flow field, and uses gradient descent to iteratively estimate optical flow. The cost function to minimize is composed of two parts:

<u>Smoothness on optical flow:</u>

<u>Brightness constancy:</u>

<u>The overall cost function:</u>

Below is a pseudocode algorithm for Horn-Schunck optical flow:

Where the update equations are (<u>for iteration k</u>):

You may check for convergence by computing the overall cost and checking that it doesn’t change much between iterations, or you may just run the procedure for a certain number of iterations until you are satisfied with the results. <u>It may take many iterations.</u>




<strong>Experiments: </strong>

<h1>Synthetic Sphere Images</h1>

<ol>

 <li>Using sphere0.png and sphere1.png, explore the <strong>Lucas-Kanade</strong> method using a neighborhood size of <strong>3</strong>, <strong>5, 11, and 21</strong>.

  <ul>

   <li>For each neighborhood size, <u>plot optical flow as a vector field <strong>and</strong> the magnitude of the optical</u> <u>flow field at every pixel</u>.</li>

   <li>Describe the impact of the neighborhood size. Do you conclude that it plays a large role in the estimation of the optical flow field?</li>

  </ul></li>

</ol>

<strong> </strong>

<ol start="2">

 <li>Using sphere0.png and sphere1.png, explore the <strong>Horn-Schunck </strong>method using values of <a href="https://en.wiktionary.org/wiki/%CE%BB">λ</a> = <strong>100, 10, 1, and 0.1</strong>.

  <ul>

   <li>For each value of <a href="https://en.wiktionary.org/wiki/%CE%BB">λ</a><a href="https://en.wiktionary.org/wiki/%CE%BB">,</a> <u>plot optical flow as a vector field <strong>and</strong> the magnitude of the optical flow field</u> <u>at every pixel</u>.</li>

   <li>Describe the impact of <a href="https://en.wiktionary.org/wiki/%CE%BB">λ</a><a href="https://en.wiktionary.org/wiki/%CE%BB">.</a> Do you conclude that it plays a large role in the estimation of the optical flow field?</li>

  </ul></li>

</ol>

<strong> </strong>

<h1>Real Traffic Images</h1>

<strong> </strong>

<ol start="3">

 <li>Using traffic0.png and traffic1.png, get the best results you can using the <strong>Lucas-Kanade</strong>

  <ul>

   <li>Show the best result you were able to obtain along with any parameter values used. <u>Plot optical</u> <u>flow as a vector field <strong>and</strong> the magnitude of the optical flow field at every pixel</u>.</li>

   <li>Discuss the process of obtaining good results, i.e. was it easy/difficult?</li>

  </ul></li>

</ol>

<strong> </strong>

<ol start="4">

 <li>Using traffic0.png and traffic1.png, get the best results you can using the <strong>Horn-Schunck </strong>

  <ul>

   <li>Show the best result you were able to obtain along with any parameter values used. <u>Plot optical</u> <u>flow as a vector field <strong>and</strong> the magnitude of the optical flow field at every pixel</u>.</li>

   <li>Discuss the process of obtaining good results, i.e. was it easy/difficult?</li>

  </ul></li>

</ol>

<strong> </strong>

<h1>Summary</h1>

<strong> </strong>

<ol start="5">

 <li>Give your overall thoughts of the two methods:</li>

</ol>

<ul>

 <li>Do each have certain strengths and weaknesses, or is there one method that you find to be superior?</li>

 <li>Compare the methods in terms of difficulty in choosing parameters.</li>

 <li>Compare the methods (qualitatively) in terms of run time.</li>

 <li>Were both methods equally challenging to implement. Did you find one to be easier?</li>

</ul>

<strong>Helpful hints: </strong>

<strong> </strong>

<ul>

 <li><strong>Plotting vectors over an image</strong></li>

</ul>




# Subsample the vector field to make it less dense subsample = 6 sub_u = u[0:rows:subsample, 0:cols:subsample] sub_v = v[0:rows:subsample, 0:cols:subsample]

xc = np.linspace(0, cols, sub_u.shape[1]) yc = np.linspace(0, rows, sub_u.shape[0])




# Locations of the vectors xv, yv = np.meshgrid(xc, yc)

fig1 = plt.figure(figsize = (14,7))

plt.imshow(im1,cmap = ‘gray’) plt.title(‘Optical Flow’), plt.xticks([]), plt.yticks([])




# Plot the vectors plt.quiver(xv, yv, sub_u, sub_v, color=’y’)




<ul>

 <li><strong>Blurring before computing derivatives</strong></li>

</ul>

You may find you get better (or worse) results if you blur before you compute derivatives.




<ul>

 <li><strong>Downsampling input images </strong></li>

</ul>

<strong> </strong>

You may find you get better (or worse) results if you downsample the input images.




<ul>

 <li><strong>Solving Lucas-Kanade via linear least squares instead of exact solution</strong></li>

</ul>




You saw from lecture that you can construct an exact linear system via A<sup>T</sup>A and A<sup>T</sup>b. However, this matrix A<sup>T</sup>A is problematic and will cause solver errors for many pixels in the image. The real solution involves heuristics about the eingenvalues of A<sup>T</sup>A. Solving via linear least squares avoids having to deal with this issue.