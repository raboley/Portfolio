# Resume
my resume portfolio hub for open source projects

## Projects

### Dark Cloud Encyclopedia

A website dedicated to displaying images and stats for weapons obtainable in the PS2 classic Dark Cloud. The project consists of an angular web front end hosted in an s3 bucket, and a back end of microservices that take raw unlabeled images from a twitter account and label, crop and download them to an s3 bucket do display on the website.

#### Website

The [Dark Cloud Encyclopedia](http://www.darkcloudencyclopedia.com.s3-website-us-west-2.amazonaws.com/welcome) frontend website [(Source Code - ADO)](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/Dark-Cloud-Website) is built in angular. It uses ng-graph to display live, interactive weapon upgrade trees in a graphical chart. It also uses observables to enable real time filtering, and updating of weapons and thier images.


#### Image Management

The downloading, categorizing/naming, and cropping of images happens through lambdas/containers running in aws. The flow of an image from upload to twitter, to being read by the website with the final name and size goes through the flow of these services.

1. Find tweets
1. Download Tweets
1. Rekognize Image
1. Categorize Image
1. Crop Image

The communication between the microservices is handled by a Message Broker service that recieves and sends requests between each microservice.

##### Find Tweets

[Find Tweets](https://russellboley.visualstudio.com/Dark-Cloud-Encyclopedia/_git/find-tweets?path=%2FREADME.md&version=GBmaster) scans twitter for tweets and returns any new tweets by tweetId with the associated image urls to each image in the tweet. It compares the top 100 tweetIds vs the folders in the s3 bucket where the tweet images get downloaded to.



### Monster Hunter World Amror Optimzer

An iPad app that allows users to easily min/max armor combinations for the game monster Hunter world. Users pick their desired set of skills and the app returns the most efficient set of armor pieces/jewels to achieve that outcome.

## Education Examples

### Angular

[Angular Getting Started - Pluralsight](https://github.com/raboley/Angular-GettingStarted)

