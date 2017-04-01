Student information
----------

### Personal details ###
* **Name**: Adeel Ahmad
* **Email**: adeelahmadadl1995@gmail.com
* **GitHub handle**: adl1995
* **Timezone**: UTC +05:00
* **Blog**: http://adl1995.github.io/

### Academic details ###
* **University**: National University of Computer and Emerging Sciences, Islamabad
* **Degree**: Computer Science 
* **Graduation year**: 2018 


Background
------

In my previous semester, I enrolled myself in Digital Image Processing course. During the tenure of this course I implemented filters (Gaussian, Sobel, Prewitt, Laplacian), edge detectors (Canny, Marr Hildreth), morphological operators (Covex hulling, Erosion, Dilation), object detectors (Generalized Hough transform, simple convolution), and seam carvers. These were implemented purely in Python, making no use of external libraries other than ``Numpy`` and ``Matplotlib``. This attenuated my interest in Computer Vision and I have been an active researcher in the domain since then. I have showcased these project on my [GitHub profile](https://github.com/adl1995). The most interesting algorithm I implemented was [Generalized Hough Tranfrom](https://github.com/adl1995/generalised-hough-transform). I was amazed as to how something as simple as an equation of line could lead to detection of objects in images. Although my implementation was only scale invariant, I plan on extending this invariancy to orientation as well. 

Apart from this, I have also been a PHP web developer for almost two years, and I have worked on multitude of projects ranging for SaaS to e-commerce websites. I work remotely on [Upwork](https://www.upwork.com/freelancers/~018e56b8591046f889) and [Fiverr](https://www.fiverr.com/adl1995). My clients are either IT organizations or independent contractors. I have also worked on web automation and data scraping using ``Selenium`` and ``BeautifulSoup``. Although these skills are not required for this organization and have no direct links in my proposed project, it shows that I am persistent and hard-working. The skills that I acquire are through self learning and consistency. Currently I am building an application using [Google Application Engine](https://github.com/adl1995/zoho-portal).

#### Why me? ####

I started collaborating with Open Source organizations for only about a month now, and my experience has been excellent so far. The mentors have been very kind, welcoming and have provided assistance along the way. Given my background in Computer Vision and being good at problem solving, I firmly believe this prestigious organization and its users will benefit by this features' addition in the library. It would also provide me with a working ground knowledge on how to tackle things in real life.

Pull requests
-------

For the past few weeks I have made numerous commits concered with current documentation. I then opened up a Pull Request (https://github.com/opencv/opencv/pull/8253) which finally got merged. Also, I created this issue (https://github.com/opencv/opencv/issues/8260) regarding the current ``Doxygen`` documentation. My suggestion was to put all the 'repeated' information in a main view and extend sub-views from it. This saves time and allows the editor to make changes in only one file. Although these are all documentation changes, I believe them to be crucial for new users of OpenCV or any tool for that matter. It creates a 'welcoming' sense for the user. 

Apart from this, I created some C++ scripts locally utilizing the various features offered by OpenCV. 

Project details
--------

### Research paper ###
> [Fast Detection of Curved Edges at Low SNR](https://arxiv.org/pdf/1505.06600.pdf)

### Problem statement ###

Let's elaborate on edge detection in noisy images.
> Edge detection is a fundamental concept in the field of Computer Vision. Its application varies from detecting shapes, images filters, and edge enhancement. However, the introduction of noise in an image makes the process error prone and much difficult. The algorithm proposed in this paper tries to overcome this.

### Use cases ###
Low signal-to-noise ratio images mostly occur under poor visibility conditions. They mostly occur in
``biomedical``, ``satellite``, ``underwater``, and high shutter speed imaging. It is crucial for these images to be viewed under better conditions, thus the addition of this algorithm will provide assisstance to the members of these communities. 

### Abstract ###

When dealing with noisy images, different approaches are adopted, such that it does not degrade the content of an image. Mostly, a Canny Edge detector is used for this purpose, which first applies a Gaussian filter to smooth out the image, and then computes its gradients. It effectively attenuates the noise in an image through its application. Different approaches are used for this problem. Some algorithms denoise an image prior to edge detection, but this does not provide improved results.

The approach that I plan to implement (mentioned in the [CVPR paper](https://arxiv.org/pdf/1505.06600.pdf)) detects faint edges in an image. This is done by applying a collection of matched filters to the image, and then retaining / keeping only those edges that are statistically significant. When an actual edge is detected, it faints out surrounding noise from the region. The longer the edge, the more noise gets attenuated, hence it does not suffer degradation from other general purpose filters.

The algorithm mentioned below has proven to be numerous magnitude times faster than other methods dealing with high noise level. 

### Detailed description ###

Edge detection filters proposed by Sobel, Prewitt, and Marr & Hildreth are although effective for computing edges, they are somewhat invariant to noisy images. As the images we will work with have low signal-to-noise ratio (SNR), these algorithms do not perform well on them. An exception to this is Canny, it performs hysteresis thresholding of local gradient magnitudes. This post-processing technique improves its accuracy. 

The algorithm proposed in this paper first denoises an image. Image denoising can be done in a number of ways. In the recent years bilateral filtering, anisotropic diffusion, non-local means have been used. These methods, however, only denoise an image in patches. I plan on implementing a ``wavelet based edge detection`` method.

A wavelet based edge detector has advantages over other traditional filters because they can vary in length and width, i.e they can be scaled. So, this detector effectively allows us to control their behavior. A careful balance is to be set between the image resolution and the scale of edges. Sharper edges are retained by the wavelet transform across different scales, whereas less significant edges are attenuated as the scale increases.

There are two approaches mentioned in the research paper. They both work on a binary tree partition, and then performs processing on it. The first method requires ``O(N<sup>1.5</sup>)`` time complexity and produces better results, the other method has a ``O(N log(N))`` complexity and results in a slight loss of detection accuracy but is faster, I propose to implement both of these. The execution time of the latter 'faster' algorithm is 2 seconds on a (129x129) image. Alternatively, the run time is several minutes per image in the paper ["Detecting Faint Curved Edges in Noisy Images"](https://pdfs.semanticscholar.org/9d5b/a5041f2063db2bc110dbb40c099f1f9b7ecf.pdf), by Sharon Alpert.

### Approach ###

The input image  *I* is in grayscale, which is further decomposed into "I = I<sub>clean</sub> + I<sub>noise</sub>" where I<sub>clean</sub> is a noise free image with step edges of constant contrast and I<sub>noise</sub> is a noisy image. An edge is represent by ``γ`` (gamma). The following response vector is associated with the curve γ

>φ(γ) = [R, L, C, P ]

* L: total length of curve γ
* P: set of pixels through which the curve passes
* C: average contrast along the curve, equates to ``R/m(L)``
* R: Difference between sum of pixel intensities along each side of curve γ

To detect curves with significant responses, a 'beam-curve binary tree' of the noisy image *I* is constructed. The tree is constructed using the bottom up approach. A pseudo code for its construction is cited below:

```
BeamCurveTree(V):
 Require: Tile V whose maximal side length is n.
  if n ≤ nmin then
     BC ← BottomLevel(V)
  else
     V1 , V2 ← SubT iles(V) { The tile is split into two
     sub-tiles of equal area}
     BC1 ← BeamCurveT ree(V1)
     BC2 ← BeamCurveT ree(V2)
     BC ← CoarserLevel(V, V1 , V2 , BC1 , BC2)
 end if
 return BC
```

Here ``BC`` is a data structure in which we store our tree. The edge map *E* is constructed by setting all points of *E* to zero. Then, we assign it with significance scores based on φ(γ), as I described earlier. After this all curves are sorted in descending order. For each curve γ in this sorted list,
for each pixel *p ∈ P*, *E(p)* is set to hold the score of γ. Non-maximum suppression is then applied to deal with over lapping curves.

There are two alternatives to binary beam tree, namely  Triangle-Partition-Tree (TPT) and  the Rectangle-Partition-Tree (RPT). A TPT is usually computationaly faster. In RPT the square matrix is recursively broken down into smaller matrices uptil our n<sub>min</sub> has been reached. As the name denotes, for TPT the image is broken down into smaller triangles. Both these yield a similar edge detection performance.

#### Results ####
As mentioned in the paper, experiments were conducted on images with different SNR levels. Image of the letter 'S' was used for this purpose. Different SNR levels of 0.6 and 2.6 in intervals of 0.2 were chosen. Futhermore, salt and pepper noise was added in the image. This only affect around 1% of the total pixels. The F-measure was computed and compared with results achieved through other algorithms. F-measure is a summary statistic for a precision-recall curve, mentioned in [this](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/papers/mfm-pami-boundary.pdf) paper. Our algorithm achieved the best score.

## Timeline ##

| Time Period        | Plan           |
| ------------- | ------------- |
| May 04, 2017 - May 30, 2017 **(Community Bonding Period)**      |   <ul><li>Read related research papers to get a more robust view of the problem.</li><li>Discuss with mentors and get a final idea on how to approach the problem.<li>Discuss with mentors on which Python package to use for GUI implementation, for example ``PyQt``.</li><li>Discuss with mentors which documentation generation tool to use. I personally prefer ``Sphinx`` over ``Doxygen``.</li></ul>|
| | **Part 1 starts** |
| May 30, 2017 - June 15, 2017 ( 2 weeks ) | <ul><li>Set up the developement environment, get familiar with OpenCV's coding practices.</li><li>Write a skeleton layout of the algorithm to implement.</li><li>Document and write tests for the added part.</li></ul> |
| June 16, 2017 - June 30, 2017 ( 2 weeks ) | <ul><li>Implement naive version of the algorithm.</li><li>Write tests cases for the implemented part.</li><li>**Update 1 : Push code so that it is possible to compute edges on a grayscale image.**</li></ul>|
| | **Part 1 completed**<br />**Part 2 starts** |
| July 01, 2017 - July 14, 2017 ( 2 weeks ) | <ul><li>Implement imporved version of the algorithm.</li><li>Add functionality that enables user to perform pre-processing on images for better results.</li><li>Add support for morpholgical operators.</li></ul> |
| July 15, 2017 - July 28, 2017 ( 2 weeks ) | <ul><li>Add optimizations, add reporting feature.</li><li>Implement GUI functionality using the proposed library.</li></ul> |
| | **Part 2 completed** |
| August 21, 2017 - August 29, 2017 **(Students Submit Code and Evaluations)** | <ul><li>Clean up code.</li><li>Improve documentation.</li><li>Add test cases.</li><li>Code refactoring (if required).</li><li>Resolve merge conflicts (if any).</li></ul> |
| August 29, 2017 - September 05, 2017 | Mentors submit final student evaluations. |
| September 06, 2017 | Results Announced. |

## Availability ##

My final exams are scheduled to end on May 20<sup>th</sup>. So, I will have ample time for the community bonding period. After that, I will be free during the whole summer i.e. almost three months. I do not have any other commitments, so I can focus all my attention to GSoC.

