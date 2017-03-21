Student information
----------

### Personal details ###
* **Name**: Adeel Ahmad
* **Email**: adeelahmadadl1995@gmail.com
* **GitHub handle**: adl1995
* ##**IRC nickname (#OpenAstronomy)**: adl1995
* **Timezone**: UTC +05:00
* **Blog**: http://adl1995.github.io/

### Academic details ###
* **University**: National University of Computer and Emerging Sciences, Islamabad
* **Degree**: Computer Science 
* **Graduation year**: 2018 


Background
------

In my previous semester, I was enrolled in Digital Image Processing course. During the tenure of this I implemented filters (Gaussian, Sobel, Prewitt, Laplacian), edge detectors (Canny, Marr Hildreth), morphological operators (Covex hulling, Erosion, Dilation), object detectors (Generalized Hough transform, simple convolution), and seam carving. These were implmented purely in Python, making on use of ``Numpy`` and ``Matplotlib``. This attenuated my interest in Computer Vision field and I have been an active researcher since then. I have showcased these project on my [GitHub profile](https://github.com/adl1995). The most interesting algorithm I implmented was [Generalised Hough Tranfrom](https://github.com/adl1995/generalised-hough-transform). I was amazed to how something as simple as an equation of line could lead to detection of objects in images. Although this was only scale invariant, I plan on extending this invariancy to orientation as well. 

Apart from this, I have also been a PHP web developer for almost two years now, and I have worked on large SaaS projects and e-commerce website. I work remotely on [Upwork](https://www.upwork.com/freelancers/~018e56b8591046f889) and [Fiverr](https://www.fiverr.com/adl1995). My clients are either IT organizations or independent contractors. I have also worked on web automation and data scraping using ``Selenium`` and ``BeautifulSoup``. Although these skills are not required for this organization and have no direct links in my proposed project, it shows that I am persistent and hard-working. The skills that I acquire are through self learning and consistency. Currently I am building an application using [Google Application Engine](https://github.com/adl1995/zoho-portal).

I have started collaborating with Open Source organizations for only about a month now, and my experience so far has been excellent. The mentors have been very welcoming and have helped provided assistance in understanding the project. 


Project details
--------

### Problem statement ###

Let's elaboarte on edge detection in noisy images.
> Edge detection is a fundamental concept in the field of Computer Vision. Its application varies from detecting shapes, images filters, and edge enhancement. However, the introduction of noise in an image makes the process error prone and much difficult. The algorithm proposed in this paper tries to overcome that.

### Abstract ###

When dealing with noisy images, different approaces are adopted, so it does not degrade the content of an image. Mostly, a Canny Edge detector is used for this purpose, which first applies a Gaussian filter to smooth out the image, and then computes its gradients. It effectively attenuates the noise in an image through the application of Gaussian filter. Different approaces are used for this problem. Some algrothims denoise the image prior to edge detection, but this does not provide imporved results.

The approach that I will implement (mentioned in the [CVPR paper](https://arxiv.org/pdf/1505.06600.pdf)) detects faint edges in an image. This is down by applying a collection of matched filters to the image, and then retaining / keeping only those that are statisticaly significant. When an actual edge is detected through this curves, it faints out surrounding noise from the region. The longer the edge is, the noise gets more attenuated, hence it does not suffer degradation from other general purpose filters 

The algorithm mentioned below proven to be numerous magnitudes time faster than other methods dealing with high noise level. 


## Prior experience ##

## Problem outline ##
-------------------

## Use cases ##
-------------

High noise images usualy arise when in biomedical satelites application. As the images are captured with a 
high shutter speed, this leads to an increased level of noise content.

## Traditional approach ##
------------------------

When dealing with high noise images, different approaces are adopted, so it does not suffer degradation of the general purpose noise.

## Alternative approach ##

As it takes a long time to detect all edges using the traditional approach. I plan on implementing a different algorithm (mentioned in **this** CVPR paper) which tackles the problem differently. This algorithm will work on heirarchical binary patters. It constructs matched filters for detected edges using the bottom up approach. ... so it runtime is linear.

We calculate the response scores. ... There a two ways to solve this, either by using rectangular or triangular partitioning.

## Timeline ##

| Time Period        | Plan           |
| ------------- | ------------- |
| April 22, 2016 - May 22, 2016 **(Community Bonding Period)**      |   <ul><li>Read documentation and get more familiar with how Fido works.</li><li>Discuss with mentors and get a final idea of how to approach the project.<li>**Get familiar with the various clients that Fido would be supporting and also understand how each client’s query is different from other clients and how to download data from each client.** This is important because later on one common query will have to be assigned to a client automatically, and downloads from that particular client will be made.</li><li>**Discuss with mentors and get a final idea of which client will serve which kinds of files and decide how the metadata of each file type will be stored in the database. Also finalize how to store metadata of any file types which are not currently supported ( maybe create an additional feature that will allow easy additions of new file types’ metadata to the database in the future ).**</li><li>Read code and get more familiar with the caching mechanism and try to get an idea of what challenges could possibly arise while implementing the new caching mechanism. This is important because query results of multiple clients will be stored in the cache.</li></ul>|
| | **Part 1 starts** |
| May 23, 2016 - May 29, 2016 ( 1 week ) | <ul><li>**Implement adding the Fido records to the database.**</li><li>Ensure that functionalities like `display_entries` etc. are working. Cross check by adding entries using specific client methods (the old way).</li><li>Document and write tests for adding while using Fido.</li><li>**Update 1 : Push code which will enable the database to accept Fido records/entries.**</li></ul> |
| May 30, 2016 -  June 12, 2016 ( 2 weeks ) | <ul><li>**Implement querying with Fido.** Ensure that the different clients are recognized correctly and correct results are returned. Cross check by using custom queries for each client.</li><li>Write tests for querying with Fido.</li><li>Document querying with Fido.</li><li>**Update 2 : Push code so that querying inside the database is successfully done using Fido attributes.**</li></ul> |
| June 13, 2016 - June 20, 2016 ( 1 week ) | <ul><li>**Implement downloading files for VSO and HEK queries after querying database.**</li><li>Ensure that the correct files from the correct clients are being downloaded by checking using the old separate download functions.</li></ul> |
| **June 21, 2016 - June 28, 2016 (Midterm Evaluations / Buffer period)** | **Mid term deliverables :**<ul><li>Querying with Fido</li><li>Adding Fido records to the database</li><li>Downloading files from VSO and HEK queries using Fido. Downloading using other clients, tests and documentation will be done after mid-term evaluations.</li><li>Continue work on downloading files using Fido.</li></ul> |
| June 28, 2016 - July 4, 2016 ( 1 week ) | <ul><li>**Implement downloading files for all other remaining clients.**</li><li>**For all supported file types, implement storing their metadata in the database. The database module already handles FITS files pretty well.**</li><li>**If needed, create a new feature/wrapper which will allow new file types’ metadata to be added easily to the database in the future.**</li><li>Cross check for every client by using the old separate download methods for downloading files.</li><li>Document and write tests for downloading files using Fido.</li><li>**Update 3 : Push code so that files from all clients can be downloaded from a Fido search result.**</li></ul> |
| July 5, 2016 - July 11, 2016 ( 1 week ) | <ul><li>**Test and ensure that all other pre-existing functionalities of the database module like `tag`, `star`, `undo` etc. are still working.**</li><li>Clean up code to make it PEP8 compliant.</li><li>Finalize Part 1 of the project after reviewing it with mentors.</li></ul> |
| | **Part 1 completed**<br />**Part 2 starts** |
| July 12, 2016 - July 25, 2016 ( 2 weeks ) | <ul><li>**Implement functionality that serializes each query result by converting them to JSON.** Make sure that the serialization and deserialization processes work correctly.</li></ul> |
| July 26, 2016 - August 8, 2016 ( 2 weeks ) | <ul><li>**Implement adding the new type of entries to the cache table in the database.**</li><li>**Implement searching through this database and check if all query results from all different clients are matching correctly.** This includes ensuring that pre-existing query results are detected correctly for every client, like VSO, HEK etc.</li><li>**Implement skipping downloading of files** in case there is a query result match in the cache.</li><li>Ensure that this “skipping” is working for all clients.</li></ul> |
| August 9, 2016 - August 15, 2016 ( 1 week ) | <ul><li>**Buffer period**</li><li>Write documentation and tests for the new caching mechanism.</li><li>**Update 4 : Push code so that the database successfully uses the new caching mechanism.**</li></ul> |
| | **Part 2 completed** |
| August 16, 2016 - August 24, 2016 **(Students Submit Code and Evaluations)** | <ul><li>Clean up code</li><li>Improve documentation</li><li>Resolve merge conflicts (if any)</li></ul> |
| August 24, 2016 - August 30, 2016 | **Mentors Submit Final Evaluations** |
| August 30, 2016 | **Results Announced** |

## Availability ##

