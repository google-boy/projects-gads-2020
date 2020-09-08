## Translation of the the lab Google Cloud fundamentals: Getting started with Compute engine

## Objectives
  -Create a Compute Engine Virtual Machine using GCP console
  -Create a  Compute Engine Virtual Machine using the gcloud command-line interface
  -Connect between the two instances

# Note:
    The lab instructions are translated to 100% command-line in this document

# 1. Create a VM named my-vm-1
        gcloud compute instances create my-vm-1 --zone=us-central1-a --machine-type=e2-medium --tags=http-server --image=debian-9-stretch-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=my-vm-1 --reservation-affinity=any

# Create a firewall rule to allow http traffic
        gcloud compute  firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server


# Create another vm in a different zone
    First list the different zones in this Region
        gcloud compute zones list | grep us-central1

    Choose a different zone from the first vm, my-vm-1
        gcloud config set compute/zone us-central1-b

    Create a vm, my-vm-2 in this new zone
        gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" 
        --image "debian-9-stretch-v20190213" --subnet "default"

# Connect between the two instances
    ssh my-vm-2
    ping c -3 my-vm-1

    result:- ping reveals the full hostname of my-vm-1, and 0% packet loss

    ssh my-vm-1

Instal nginx web server on my-vm-1
    sudo apt-get install nginx-light -y
Edit the home of the web server using nano editor
    sudo nano /var/www/html/index.nginx-debian.html
Use arrow keys to move the cursor just below the h1 header, Edit it e.g "Hi Hezron"
Save the file using CTRL+O, ENTER then CRTL+X to exit the nano editor
Confirm the web server is serving the new page
    curl http://localhost/
    The response will be the HTML source of the web server's home page, including your line of custom text.

Confirm that my-vm-2 can reach the web server on my-vm-1
    curl http://my-vm-1/
    The response will again be the HTML source of the web server's home page, including your line of custom text.

That is it, we have created two vms and tested their connectivity

