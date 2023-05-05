<div align="center">
<img src=https://static.wixstatic.com/media/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png/v1/fit/w_2500,h_1330,al_c/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png width="400" height="200">
 </div>

# <div align="center"> TERRAFORM ASSIGNMENT </p>

# <div align="center"> DevOps Instructor-led Training </div>

<br />

<br />

<br />

<br />

# $${\color{brown} &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; Contact&emsp;us: &emsp;&emsp;&emsp; }$$

<div align="right"> T O A C C E L E R A T E Y O U R C A R E E R G R O W T H </div>

### <div align="right"> For questions and more details: </div>

<div align="right"> <img src=https://w7.pngwing.com/pngs/759/922/png-transparent-telephone-logo-iphone-telephone-call-smartphone-phone-electronics-text-trademark-thumbnail.png width="20" height="20"> +91 98712 72900 </div>

<div align="right"> <img src=https://pbs.twimg.com/profile_images/1450734615946219520/jmBHQRRa_400x400.jpg width="20" height="20"> https://www.thecloudtrain.com </div>

<div align="right"> <img src=https://icons.iconarchive.com/icons/martz90/circle/512/email-icon.png width="20" height="20"> support@thecloudtrain.com </div>

<div align="right"> <img src=https://png.pngtree.com/png-vector/20221018/ourmid/pngtree-whatsapp-icon-png-image_6315990.png width="20" height="20"> +91 98712 72900 </div>

## Exercise 1: Terraform Lifecycle

## _Create a GCP ubuntu instance using Terraform_

### Complete below tasks as part of this exercise:

* Create a Terraform project and create Terraform template file to deploy a Compute instance in GCP.
* Run Terraform Plan and save the execution plan in a file and verify the changes.
* Now, apply the verified changed using apply.
* Validate the compute instance created in GCP console

## Exercise 2: Terraform Variables and Templates

### Complete below tasks as part of this exercise:

* Clone the code from GitHub repo: https://github.com/vistasunil/devopsIQ.git
* Create a docker image of this code and push it to Docker hub.
* Now, create a Terraform project to build infrastructure and deploy website using Terraform.
* Use distributed way to perform this task as below:
   * Create two GCP resource – 
     * Compute Engine, and 
     * Compute Network. 
     This compute engine should use this network only.
   * Use metadata script to install docker and deploy container webapp using the images created from GitHub code.
   * Create a separate provider file to add google provider.
   * Keep variables in a separate variable file.
   * Use separate output file to display the server public IP at the end.
* Apply the configuration using Terraform.
* Validate the resources created in GCP console.
* Copy the public IP of the server created and access the deployed containerized app on web browser.

## Exercise 3: Terraform Modules

### Complete below tasks as part of this exercise:

* Implement the Exercise 2 using Terraform modules as below:
   * First module named **compute** to create a GCP Compute Engine instance .
   * Second module names **network** to create GCP Compute Network.
* Call both the modules in main.tf file to create Compute Instance and Network. 
* Rest of the things should remain same as **Exercise 2** for implementation.
* Once everything deployed then try to access the app on web browser.
