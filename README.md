#Beer to Cats#

##Installation##
1. Ensure that you have python 2.7.5+
2. Install [pip](http://www.pip-installer.org/en/latest/installing.html)
    - On Ubuntu: `sudo apt-get install python-pip`
    - On Windows, OS X, or Ubuntu: 
        1. First, download [get-pip.py](https://raw.github.com/pypa/pip/master/contrib/get-pip.py) `$ curl https://raw.github.com/pypa/pip/master/contrib/get-pip.py`
        2. Then run `$ python get-pip.py`
3. `$ pip install -r requirements.txt` (may require `sudo`)

###Installation Errors?###


##Usage##
There are two primary ways to use the project:

1. Run the program via the command line and input images as command line parameters.
    ```
    $ python beer_to_cats.py <image.{png,jpg,jpeg,gif}> <optional threshold value>
    ```

2. Run the program on the webapp we've created. You can do that either by navigating to [BeerToCats.com](http://www.BeerToCats.com) or executing the following commands:
    ```
    $ python yolocups.py
     * Running on http://127.0.0.1:5000/
     * Restarting with reloader
    ```
Then navigate to http://127.0.0.1:5000/ and follow the instructions on the website as you would otherwise.

##Demo##


##Theory##
Let's say we have the following image where we want to find all of the solo cups and cover them with a cat. We will refer to this image in the following paragraphs.

![IceCream](/Desktop/anat-ice-cream.jpg)

There are several widely-used methods for feature detection – e.g. [Haar-like Feature Detection](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf), [Histogram-of-Oriented Gradient (HOG) Feature Detection](http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf), etc.

For this project, we chose HOG detection. Therefore, we also needed to use a [Support Vector Machine (SVM)](http://en.wikipedia.org/wiki/Support_vector_machine) as the classifier.

To get the best results, we need a training set. We peroused the web for images of cans, bottles, and solo cups. Then, since this involves supervised learning, we went through drawing boxes around all of the cans, bottles, and cups. Using the previous image, we end up with the following:

![IceCreamBox](/Desktop/anat-ice-cream-annot.jpg)

Once we have a good set of these, we generate an XML file of these images with the box annotations. From this, we then compute the HOG representation of the boxed images. We'll choose the most prominant solo cup for this example.

Before HOG:

![SoloCup](/Desktop/solo.jpg)

How the computer sees it:

![SoloCup](/Desktop/solo.jpg)

After computing the HOG of the image:

- Overlayed HOG Representation (computed using Mathematica)

    - ![SoloCupComputer](/Desktop/solo-visible-gradient.png)

- Pure HOG Representation

    - ![SoloCup](/Desktop/solo-hog.jpg)

These are fed into the SVM, with all of the possible orientations replicated and fed into the SVM as well.

###OK, so What is Histogram of Oriented Gradient (HOG)?###

###What's a Support Vector Machine (SVM)?###


##TODO##
For the project:
- Integrate with webapp

For documentation:
- Add to `requirements.txt`: Flask
- Add to `README.md`: example test run, images, and theory behind it
- Edit `README.md`: ensure instructions actually work... ugh I hate instructions that don't work.
