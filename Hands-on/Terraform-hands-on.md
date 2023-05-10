<div align="center">
<img src=https://static.wixstatic.com/media/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png/v1/fit/w_2500,h_1330,al_c/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png width="400" height="200">
 </div>

# <div align="center"> TERRAFORM HANDS-ON </p>

# <div align="center"> DevOps Instructor-led Training </div>

# <div align="right"> $`\textcolor{brown}{\text{Contact us: }}`$  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; </div>

<div align="right"> T O A C C E L E R A T E Y O U R C A R E E R G R O W T H </div>

### <div align="right"> For questions and more details: </div>

<div align="right"> <img src=https://w7.pngwing.com/pngs/759/922/png-transparent-telephone-logo-iphone-telephone-call-smartphone-phone-electronics-text-trademark-thumbnail.png width="20" height="20"> +91 98712 72900 </div>

<div align="right"> <img src=https://pbs.twimg.com/profile_images/1450734615946219520/jmBHQRRa_400x400.jpg width="20" height="20"> https://www.thecloudtrain.com </div>

<div align="right"> <img src=https://icons.iconarchive.com/icons/martz90/circle/512/email-icon.png width="20" height="20"> support@thecloudtrain.com </div>

<div align="right"> <img src=https://png.pngtree.com/png-vector/20221018/ourmid/pngtree-whatsapp-icon-png-image_6315990.png width="20" height="20"> +91 98712 72900 </div>

## TERRAFORM

## _Terraform Installation_

Refer [Official installation page](https://developer.hashicorp.com/terraform/downloads) for installation steps.

### _Set up GCP_

* **A GCP Project**: GCP organizes resources into projects. Create one if it doesn’t exists in the GCP console and make note of the project ID. 
* **Google Compute Engine**: Enable Google Compute Engine for your project in the GCP console (if not enabled). Make sure to select the project you are using to follow this tutorial and click the "Enable" button.
* **A GCP service account key**: Create a service account key or use existing one to enable Terraform to access your GCP account. When creating the key, use the following settings:
  * Select the project you created in the previous step.
  * Click "Create Service Account".
  * Give it any name you like and click "Create".
  * For the Role, choose "Project -> Editor", then click "Continue".
  * Skip granting additional users access, and click "Done".
* After you create your service account, download your service account key.
  * Select your service account from the list.
  * Select the **Keys** tab.
  * In the drop-down menu, select **Create new key**.
  * Leave the **Key Type** as JSON.
  * Click **Create** to create the key and save the key file to your system.	

_**Warning**: The service account key file provides access to your GCP project. It should be treated like any other secret credentials. Specifically, it should never be checked into source control._

## _Create a GCP resource using Terraform_

### _Create Configuration_

### Step 1: The set of files used to describe infrastructure in Terraform is known as a Terraform *configuration*. You will now write your first configuration to create a network.

Each Terraform configuration must be in its own working directory. Create a directory for your configuration.

`mkdir terraform-gcp`

### Step 2: Change into the directory.

`cd terraform-gcp`

![image](https://user-images.githubusercontent.com/37858762/236444896-666d79c9-6d74-4c40-8c2d-5000841d6e25.png)

### Step 3: Terraform loads all files ending in .tf or .tf.json in the working directory. Create a main.tf file for your configuration.

`vim main.tf`

Open main.tf in your text editor, and paste in the configuration below. Be sure to replace <NAME> with the path to the service account key file you downloaded and <PROJECT\_ID> with your project's ID, and save the file.

```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "3.5.0"
    }
  }
}

provider "google" {
  credentials = file("<NAME>.json")

  project = "<PROJECT_ID>"
  region  = "us-central1"
  zone    = "us-central1-c"
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}
```

![image](https://user-images.githubusercontent.com/37858762/236444774-73376b6f-ec63-4324-92f8-c36eedfc6c2f.png)

This is a complete configuration that Terraform can apply. 

### _Initialize the directory_

### Step 4: When you create a new configuration — or check out an existing configuration from version control — you need to initialize the directory with terraform init. This step downloads the providers defined in the configuration.

Initialize the directory.

`terraform init`

![image](https://user-images.githubusercontent.com/37858762/236444743-a89f80b4-4422-469c-b1c3-e9999be9a909.png)

### _Format and validate the configuration_

### Step 5: We recommend using consistent formatting in all of your configuration files. The terraform fmt command automatically updates configurations in the current directory for readability and consistency.

Format your configuration. Terraform will print out the names of the files it modified, if any. In this case, your configuration file was already formatted correctly, so Terraform won't return any file names.

`terraform fmt`

![image](https://user-images.githubusercontent.com/37858762/236444730-8e910601-c2ce-46a6-8423-56e3a0333ea7.png)

### Step 6: You can also make sure your configuration is syntactically valid and internally consistent by using the terraform validate command.

Validate your configuration. The example configuration provided above is valid, so Terraform will return a success message.

`terraform validate`

![image](https://user-images.githubusercontent.com/37858762/236444700-61a933ec-7b39-4773-9e90-68e04c0271c7.png)

### _Create infrastructure_

### Step 7: Apply the configuration now with the terraform apply command. Terraform will print output similar to what is shown below. We have truncated some of the output for brevity.

`terraform apply`

![image](https://user-images.githubusercontent.com/37858762/236444679-0a750a86-5034-4ead-889c-78ed41a3fd5f.png)

Terraform will now pause and wait for approval before proceeding. If anything in the plan seems incorrect or dangerous, it is safe to abort here with no changes made to your infrastructure.

In this case the plan looks acceptable, so type yes at the confirmation prompt to proceed. It may take a few minutes for Terraform to provision the network.

_**Enter a value: yes**_

You have now created infrastructure using Terraform! Visit the GCP console to see the network you provisioned. 

![image](https://user-images.githubusercontent.com/37858762/236444643-337e86ae-0112-4c0b-be52-9819c4aa5b6e.png)
  
Make sure you are looking at the same region and project that you configured in the provider configuration.

### _Inspect state_

### Step 8: When you applied your configuration, Terraform wrote data into a file called terraform.tfstate. Terraform stores the IDs and properties of the resources it manages in this file, so that it can update or destroy those resources going forward.

The Terraform state file is the only way Terraform can track which resources it manages, and often contains sensitive information, so you must store your state file securely and distribute it only to trusted team members who need to manage your infrastructure. 

In production, we recommend storing your state remotely with Terraform Cloud or Terraform Enterprise. Terraform also supports several other remote backends you can use to store and manage your state.

Inspect the current state using terraform show.

`terraform show`

![image](https://user-images.githubusercontent.com/37858762/236444581-d2125ce5-0337-403c-9167-533e494e9afe.png)

When Terraform created this network, it also gathered its metadata from the Google provider and recorded it in the state file. 

### _Delete Resource_

### Step 9: Use terraform destroy to delete all the resources created through terraform template:

`terraform destroy`

![image](https://user-images.githubusercontent.com/37858762/236444561-792425fa-afd1-4683-b15e-a4c31f40befc.png)

Visit the GCP console to verify the network is deleted:

![image](https://user-images.githubusercontent.com/37858762/236444542-e918d124-3cae-4b14-9aaf-5ee5ef51714c.png)

## _Terraform State_

### _State list_

shows the resource addresses for every resource Terraform knows about in a configuration, optionally filtered by partial resource address.

`terraform state list`

![image](https://user-images.githubusercontent.com/37858762/236444521-eec674d7-789a-497a-b92a-d0f26ab2458f.png)

###  _State show_

displays detailed state data about one resource.

`terraform state show <Resource Address>`

![image](https://user-images.githubusercontent.com/37858762/236444506-fc026d7d-8509-4f23-9e19-6bba4fe46df5.png)

### _State pull_

Pull current state and output to stdout

`terraform state pull`

![image](https://user-images.githubusercontent.com/37858762/236444478-1777c65e-8060-4727-9a8c-e32bf8eff545.png)

## _Terraform Variables_

### _Create and deploy a webserver installed compute instance in GCP_

- You can create new resources by adding them to your Terraform configuration and running terraform apply to provision them.
- Note: The order in which resources are defined in your configuration files does not affect how Terraform provisions your resources, so you should organize your configuration however is easiest for you and your team to manage.

### Step 1: Create a Linux directory for the Terraform project.

`mkdir terraform-webserver`

`cd terraform-webserver`

![image](https://user-images.githubusercontent.com/37858762/236444445-5a033fa7-cd09-48e1-bc12-f4235c56eee3.png)

### Step 2: Define a Terraform Google Provider.

`vim provider.tf`

### Step 3: This file has the following content. Replace <NAME> with your svc account json key file name with location:

```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "3.5.0"
    }
  }
}

# Specify the GCP Provider
provider "google" {
  credentials = file("/home/ubuntu/<NAME>.json")
  project = var.project_id
  region  = var.region
}

```

![image](https://user-images.githubusercontent.com/37858762/236444422-8851bcb0-4e7b-4b9d-ab90-f3b8abb40a9f.png)

### Step 4: Write this Terraform code to create a Google Compute VM Instance.

`vim webserver.tf`

### Step 5: To use the latest ubuntu disk, we can use the data source:

```
data "google_compute_image" "ubuntu" {
  family  = "ubuntu-1804-lts"
  project = "ubuntu-os-cloud"
}

# Creates a GCP VM Instance.
resource "google_compute_instance" "webserver" {
  name         = var.name
  machine_type = var.machine_type
  zone         = var.zone
  tags         = ["http-server"]
  labels       = var.labels

  boot_disk {
    initialize_params {
      image = data.google_compute_image.ubuntu.self_link
    }
  }

  network_interface {
    network = "default"
    access_config {
      // Ephemeral IP
    }
  }

  metadata_startup_script = data.template_file.nginx.rendered
}
```
**Note: To allow HTTP connection to VM instance, we put the http-server tag on the VM as _tags = ["http-server"]_.**

### Step 6: Now, let's define a template file which has a script to install NGINX server and create a simple webpage index.html

`mkdir template`

`vim template/install_nginx.tpl`

```
#!/bin/bash
set -e
echo "*****    Installing Nginx    *****"
apt update
apt install -y nginx
ufw allow '${ufw_allow_nginx}'
systemctl enable nginx
systemctl restart nginx

echo "*****   Installation Completed!!   *****"

echo "Welcome to Google Compute VM Instance deployed using Terraform!!!" > /var/www/html/index.html

echo "*****   Startup script completes!!    *****"
```

_**Note: We pass the value of '${ufw\_allow\_nginx}' from the Terraform code during template rendering**_.

### Step 7: Let’s, render the above template. 

`vim webserver.tf`

Append the following code.

```
data "template_file" "nginx" {
  template = "${file("${path.module}/template/install_nginx.tpl")}"

  vars = {
    ufw_allow_nginx = "Nginx HTTP"
  }
```

Final webserver.tf will looks like below:

![image](https://user-images.githubusercontent.com/37858762/236444351-1ff3d3d5-7491-4989-bc52-154574a772e7.png)

### Step 8: Once the instance comes up, we want to know its public IP so that we can browse the webpage. To do this, we can use terraform outputs.

`vim outputs.tf`

```
output "webserver_ip" {
  value = google_compute_instance.webserver.network_interface.0.access_config.0.nat_ip
}
```

![image](https://user-images.githubusercontent.com/37858762/236444332-67c31f22-4adf-48f9-a6ed-6e523975cc0b.png)

### Step 9: Now, define all the variables in a file.

`vim variables.tf`

```
variable "project_id" {
  description = "Google Cloud Platform (GCP) Project ID."
  type        = string
}

variable "region" {
  description = "GCP region name."
  type        = string
  default     = "europe-west1"
}

variable "zone" {
  description = "GCP zone name."
  type        = string
  default     = "europe-west1-b"
}

variable "name" {
  description = "Web server name."
  type        = string
  default     = "my-webserver"
}

variable "machine_type" {
  description = "GCP VM instance machine type."
  type        = string
  default     = "f1-micro"
}

variable "labels" {
  description = "List of labels to attach to the VM instance."
  type        = map
}
```

### Step 10: Define require variables value in terraform.tfvars file.

`vim terraform.tfvars`

```
project_id = "<gcp-project-id>"
labels     = {
  "environment" = "test"
  "team"        = "devops"
  "application" = "webserver"
}
```

![image](https://user-images.githubusercontent.com/37858762/236444288-c6e5aa4b-cde2-4010-b652-c0981780d79f.png)

### Step 11: We now have the required Terraform configuration. So, let’s initialize the Terraform project.

`terraform init`

![image](https://user-images.githubusercontent.com/37858762/236444270-4ddcccba-ea4a-4f0f-bf14-44064b462fe8.png)

### Step 12: After successful initialization, run plan and save plan in a file

`terraform plan --out webserver.plan`

![image](https://user-images.githubusercontent.com/37858762/236444256-d48d2a6b-eea2-4023-bc80-39af23b1d6bf.png)

![image](https://user-images.githubusercontent.com/37858762/236444244-f9fdcb39-c2be-4230-8654-8dd217c6188b.png)

### Step 13: Plan shows to create a VM instance and use `install\_nginx.tpl` as startup script. So, let's go ahead and apply the plan.

`terraform apply webserver.plan`

![image](https://user-images.githubusercontent.com/37858762/236444221-5c3020a1-b334-4473-b08d-a68b8a490d98.png)

### Step 14: Now if you navigate to the [Google Console](https://console.cloud.google.com/) and navigate to Compute Engine --> VM Instance, you will see an instance coming up. Once the instance is up successfully, browse the webserver\_ip. In this case, go to **http://104.199.81.192**

![image](https://user-images.githubusercontent.com/37858762/236444200-3db2951e-a8fd-4132-b900-e43ab319edfb.png)

## _Terraform Modules_

### _Create and deploy a compute instance in GCP using Module_

### Step 1: Create a Linux directory for the Terraform project and cd to it.

`mkdir terraform-module`

`cd terraform-module`

![image](https://user-images.githubusercontent.com/37858762/236444172-5ba1a1c6-ec69-458b-a21c-7b24659fdcbd.png)

### Step 2: Create a Linux directory for the Terraform module inside project folder.

`mkdir compute`

`cd compute`

### Step 3: Create a configuration file for this module with same name as module i.e. compute.tf to create a compute instance and vpc network resources on GCP.

`vim compute.tf`

```
variable "computeName" {
    type = string
}

resource "google_compute_instance" "webserver" {
  name         = var.computeName
  machine_type = "f1-micro"

  boot_disk {
    initialize_params {
      image = "ubuntu-os-cloud/ubuntu-1804-lts"
    }
  }

  network_interface {
    network = google_compute_network.vpc_network.name
    access_config {
    }
  }
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}


output "webserver_ip" {
  value = google_compute_instance.webserver.network_interface.0.access_config.0.nat_ip
}
```

![image](https://user-images.githubusercontent.com/37858762/236444136-d3d27be8-cee4-4668-87b9-8d3ad54b1397.png)

### Step 4: Go to main project folder and create main.tf file. This main file will call module compute inside using module keyword and block:

`cd ..`

`vim main.tf`

```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "3.5.0"
    }
  }
}

provider "google" {
  credentials = file("<CREDENTIAL_FILE>.json")

  project = "devops-314416"
  region  = "us-central1"
  zone    = "us-central1-c"
}

variable "instance-name"{
  type = string
}

module "compute_module" {
    source = "./compute"
    computeName = var.instance-name
}

output "public_ip" {
    value = module.compute_module.webserver_ip
}
```

![image](https://user-images.githubusercontent.com/37858762/236444112-008b7515-c918-4d8d-ba11-ec25a5011b2b.png)

### Step 5: We now have the required Terraform configuration. So, let’s initialize the Terraform project.

`terraform init`

![image](https://user-images.githubusercontent.com/37858762/236444094-ed58e3db-0f38-4472-86b1-c919880b1223.png)

### Step 6: After successful initialization, run plan and save plan in a file

`terraform plan --out module.plan`

![image](https://user-images.githubusercontent.com/37858762/236444082-3e410e3a-1c89-41fc-bd1f-80c02a3681b4.png)

### Step 7: Plan shows to create a VM instance using compute module. So, let's go ahead and apply the plan.

`terraform apply module.plan`

![image](https://user-images.githubusercontent.com/37858762/236444056-ce7cfcc0-488e-4785-a2f5-371b83a60067.png)

### Step 8: Now if you navigate to the [Google Console](https://console.cloud.google.com/) and navigate to Compute Engine --> VM Instance, you will see an instance coming up with the name provided. 

![image](https://user-images.githubusercontent.com/37858762/236444042-4400b33b-4826-4df1-a5b5-999e301f6253.png)
