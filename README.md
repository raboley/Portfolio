# Resume
my resume portfolio hub for open source projects

## Projects

### Dark Cloud Encyclopedia

A website dedicated to displaying images and stats for weapons obtainable in the PS2 classic Dark Cloud. The project consists of an angular web front end hosted in an s3 bucket, and a back end of microservices that take raw unlabeled images from a twitter account and label, crop and download them to an s3 bucket do display on the website.

#### Website

The [Dark Cloud Encyclopedia - Production site](http://www.darkcloudencyclopedia.com.s3-website-us-west-2.amazonaws.com/welcome) frontend website [(Source Code - ADO)](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/Dark-Cloud-Website) is built in angular. It uses ng-graph to display live, interactive weapon upgrade trees in a graphical chart. It also uses observables to enable real time filtering, and updating of weapons and thier images.

#### Image Management

The downloading, categorizing/naming, and cropping of images happens through lambdas/containers running in aws. The flow of an image from upload to twitter, to being read by the website with the final name and size goes through the flow of these services.

1. Find tweets
1. Download Tweets
1. Categorize Image
1. Crop Image

The communication between the microservices is handled by a Message Broker service that recieves and sends requests between each microservice.

##### Find Tweets

[Find Tweets - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/find-tweets?path=%2FREADME.md&version=GBmaster) scans twitter for tweets and returns any new tweets by tweetId with the associated image urls to each image in the tweet. It compares the top 100 tweetIds vs the folders in the s3 bucket where the tweet images get downloaded to.

Depricated:

[new-twitter-image-alert - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/New-Twitter-Image-Alert?path=%2Fhandler.py&version=GBmaster&_a=history) does a similar thing, but is a lambda function and calls download tweets directly.
I went away from this approach because it made it hard to acceptance test Download tweets and anything downstream since downloading was tightly coupled. TODO: This will be deleted once I set Find Tweets up to be a lambda and/or container.

[find-new-twitter-images](https://github.com/raboley/find-new-twitter-images) also does a similar thing, but is the first iteration. It has some useful docs for how to use serverless, as well as a good example. TODO: make find-tweets serverless as well and delete this repo

[downloadTwitterImages](https://github.com/raboley/downloadTwitterPictures) The first effort that I cloned and repurposed from another person's repo. It has some CICD setup docs, but should be deleted. TODO: Migrate the docs and delete the repo.

##### Download Tweets

[Download tweets - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/download-images) is a lambda function that downloads images from a url to a specified location.

##### Categorize Images

[Categorize Images](https://github.com/raboley/categorize-images) Scans the images for text and then labels the image based on the text in the image as well as text in images related by tweetId. Images are named by the weapon indicated in the image, the character that weapon belongs to and the type of image it is. There are 3 types; Stat screen, Main Screen and Side view. The Stat screen image has the mos reliable placement of the weapon name, so first thing that is done is to determine what type of image it is. If it is a stat screen then attempt to match the name in the most likely positions with a weapon name from the list of weapons. Once the match is found it is stored in a json file in the s3 bucket with the tweet id, and weapon/character combo. Since all weapons in a single tweet should be of the same weapon, any non-stat screen images will then try to find thier own weapon name by matching their tweetId to the tweetId in the weapon map file in the s3 bucket.

##### Crop Images

There are two different services that handle cropping the images. This is so that they could scale independently.

[image-manipulation](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/image-manipulation): Crops out the black bars from images, and creates a thumbnail for the weapon then places all the images with proper names into the final bucket where the production website looks for images.

[image-manipulation-crop-blackbars](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/image-manipulation-crop-blackbars): Crops the black bars of an image using known coordinates and places the image in the final s3 bucket where the website hosts it's images. Might get rid of this, since I don't think the scalability is worth the complexity it adds.

### Monster Hunter World Amror Optimzer

[Monster Hunter World Armor Optimizer](https://github.com/raboley/MHWArmorSkillOptimizer) is an iPad app that allows users to easily min/max armor combinations for the game monster Hunter world. Users pick their desired set of skills and the app returns the most efficient set of armor pieces/jewels to achieve that outcome.

### Let It Die Calculators

[Let It Die Calculators](https://github.com/raboley/LetItDieCalculators) is a website to calculate the required materials for researching upgrades in the game Let it Die.

## Support Libraries

### Python

#### File

[File](https://github.com/raboley/File) is a wrapper around file related actions. It has two classes OS and s3. The OS class deals with reading, writing and moving of files in the local file system, while s3 handles the same operations, but in an s3 bucket. The reason I have these is so that for testing I can use dependency injection to pass in the OS class to manipulate the local file system of my dev machine, and inject the s3 class for production so that it can appropriately use the s3 buckets instead. That way the calls are done the same way in python code minimizing business code logic differences betwee dev and prod.

## Proof of Concept

[Provision-Resources - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/Provision-Resources): Creates the ec2 instances in aws to host kubernetes.

[Create-k8-Cluster - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/Create-k8-Cluster): Installs and configures kubernetes on the provisioned resources in AWS.

[Ansible-Pipeline - ADO](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/Ansible-Pipeline?path=%2Fkubernetes-deploy&version=GBmaster): Deploys the container app to the kubernetes cluseter as a deployment.


## Education Examples

[Angular Getting Started - Pluralsight](https://github.com/raboley/Angular-GettingStarted): angular basics, components, routing, etc
[TDDAngularMovieApp -Pluralsight](https://github.com/raboley/TDDAngularMovieApp): writing TDD angular code using karma and jasmine

[AWS Developer Getting Started - Pluralsight](https://github.com/raboley/AWSDeveloper-GettingStarted/blob/master/pizza-luvrs/HelpMe.md): AWS basics, security, ec2, s3, etc.

[Docker Ansible CICD - Pluralsight](https://github.com/raboley/docker-ansible): Full CICD pipeline for python app using docker and asnible.

[Puppet fundamentals - Pluralsight](https://github.com/raboley/puppet-fundamentals-lab/tree/master): Puppet basics on puppet server, code and dev environment setup.