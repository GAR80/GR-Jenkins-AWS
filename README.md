# GR-Jenkins-AWS
Github-Jenkins-AWS data pipeline
When code is pushed to GitHub a Jenkins build process starts that deploys code to a staging AWS EC2 instance. Once deployed and reviewed the Jenkins user may then approve the deployment to production, that is done through an input request on the build screen in Jenkins. 

Production write node web server /var/www/html directory is mounted to an EFS file system, a web server AMI was created that also maps the /var/www/html directory to the same EFS share,  the AMI was then used to build a launch configuration using an ASG to launch a minimum of 3 instances at all times. The ASG is attached to an Elastic Load balancer, Route 53 has been used to attach put the URL of the load balancer behind my domain name devzonetest.com 
Everything is built on a custom VPC. 
