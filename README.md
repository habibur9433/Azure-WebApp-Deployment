# Deploying a Web Application on an Azure VM using Azure CLI
# Introduction
***In this project, I deployed a web application on an Azure Virtual Machine (VM). This is a common approach for businesses and developers who need scalable, flexible, and cost-effective infrastructure.
Azure VMs allow for customizable configurations that ensure optimal performance and reliability. Below, I outline the pros and cons of this approach.***
  
**Pros:**  
***Scalability: Easily scale resources to meet the application's demand.  
Flexibility: Full control over the VM environment to meet specific needs.  
Reliability: Azure’s infrastructure ensures high availability.  
Security: Built-in security features protect the application***.  
**Cons:**  
***Cost: Running VMs can be more expensive than PaaS alternatives.  
Management: Requires continuous maintenance and monitoring of the VM.  
Complexity: Initial setup and configuration can be challenging.***  

# Step-by-step process  

**Step 1: Create an Azure VM**  

**Log in to Azure**  
`az login --tenant <Tenant_ID>`  

![image](https://github.com/user-attachments/assets/84c2f61a-6936-46ab-a00d-666a2fb21f02)


**Create a resource group**  
`az group create --name rg-webapp --location westus`  

![image](https://github.com/user-attachments/assets/b55d0c17-8249-4c75-822b-12b03c12d6f3)


**Create a virtual machine with username and password**  
`az vm create --resource-group rg-webapp --name WebAppVM --image Ubuntu2204   --admin-username webuser --admin-password Password123456789@`  

![image](https://github.com/user-attachments/assets/e2e4f47e-f12e-4be0-91c8-997c55ecfb42)  



**Step 2: Open Ports for Web Traffic**  

**Open port 80 for HTTP and port 443 for HTTPS traffic**  
`az vm open-port --resource-group rg-webapp --name WebAppVM --port 80-500 --priority 100`  

![image](https://github.com/user-attachments/assets/393c8a74-91c9-48c1-b41f-327703292b94)
![image](https://github.com/user-attachments/assets/69445237-1b67-494c-a6e2-715afd47cd04)



**Step 3: Connect to the VM**  

**SSH into the VM**  
`ssh webuser@<public-ip-address>`  

![image](https://github.com/user-attachments/assets/56a9a03d-54e8-4ae6-85a1-ae77ac643b35)


**Step 4: Install Web Server**  

**Update package lists**  
`sudo apt-get update`  

![image](https://github.com/user-attachments/assets/61492c75-3035-4f5a-bb1d-3a8ba8d508a2)


**Install Nginx web server**  
`sudo apt-get install nginx -y`  

![image](https://github.com/user-attachments/assets/b8037e92-abed-4980-ae24-7df33d3318e4)


**Step 5: Deploy Web Application**  

**Navigate to the web root directory**  
`cd /var/www/html`  
**Remove the default Nginx page**  
`sudo rm index.nginx-debian.html`   
**Create a new index.html file for your web application**

echo `"<html><body><h1>Welcome to Habib's Web Application hosted in Azure VM</h1></body></html>" | sudo tee index.html`

**Exit the SSH session**  
`exit`  

![image](https://github.com/user-attachments/assets/c1fa80c0-445c-4155-b5bf-7cc990dc292b)



**Step 6: Verify Deployment**  


**Open a web browser and navigate to http://`<public-ip-address>` to see your web application**  

![image](https://github.com/user-attachments/assets/36729c5e-a8fa-47ed-8f0e-ab0d0669b8be)


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

***Azure Portal Overview***  
***the following screenshot from Azure Portal shows all the resources associated with my web application deployment. This overview provides a comprehensive look at the virtual machine, network security group, and other relevant resources that have been created during the setup process.***  

![image](https://github.com/user-attachments/assets/578dd8c5-e6e4-4169-95f3-751c8954d30e)  


***Removing Resources***  
***After successfully deploying the web application and verifying that everything is working. It's time to clean up the resources to avoid incurring additional costs***  
`az group delete --name rg-webapp --no-wait --yes`  

![image](https://github.com/user-attachments/assets/403c40ba-deac-40c2-b0de-6b31de4f6d17)




