# Credit2go Helm Charts Repository

This site contains helm charts for credit2go kubernetes deploy usage.

## candidates repo

this repo is in development usage for dev usage.

## releases repo

this repo is in production ready for each release of application for test and production usage.


## Note
Since we use maven-helm plugin to create charts.   
it will create charts for each application releases.  
The chart version will be same as application version.  

## Site Generation
As per we configure it in Jenkins, so this project will sync with local disk on every one hour.  
That means repo will be update every one hour.