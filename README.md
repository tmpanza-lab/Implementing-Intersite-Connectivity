# Implementing InterSite Connectivity

## Objective

In this lab I explore communication between virtual networks. I will implement virtual network peering and test connections. I will also create a custom route.

*Ref 1: Architecture diagram*
 ![image](https://github.com/user-attachments/assets/151bd848-f7ca-4df8-bb27-d02b6b56c23b)


### Job Skills Learned

- Creating a virtual machine in a virtual network.
- Creating a virtual machine in a different virtual network.
- Using Network Watcher to test the connection between virtual machines.
- Configuring virtual network peerings between different virtual networks.
-  Using Azure PowerShell to test the connection between virtual machines.
- Creating a custom route.

### Tools Used

- Azure portal - https://portal.azure.com


## Steps

## Task 1: Create a core services virtual machine and virtual network
In this task, you create a core services virtual network with a virtual machine.
1.	Sign in to the Azure portal - https://portal.azure.com.
2.	Search for and select Virtual Machines.
3.	From the virtual machines page, select Create then select Azure Virtual Machine.
![image](https://github.com/user-attachments/assets/f44f1395-65d5-4232-9f6d-37e2c112ed05)
![image](https://github.com/user-attachments/assets/ee8555b1-2b48-4b34-8088-73295b93c49f)
 
 
4.	On the Basics tab, use the following information to complete the form, and then select Next: Disks >. For any setting not specified, leave the default value.
![image](https://github.com/user-attachments/assets/6284d83d-b19a-4128-8196-3281358b5207)
 
5.	On the Disks tab take the defaults and then select Next: Networking >.
6.	On the Networking tab, for Virtual network, select Create new.
7.	Use the following information to configure the virtual network, and then select Ok. If necessary, remove or replace the existing information.
![image](https://github.com/user-attachments/assets/7693008c-77ff-455d-9135-243b978087db)
![image](https://github.com/user-attachments/assets/d6557171-fc1f-4240-bd6e-0274a58c472c)
 
 
8.	Select the Monitoring tab. For Boot Diagnostics, select Disable.
![image](https://github.com/user-attachments/assets/a811108d-84ae-487d-9ce3-d401d975407e)
 
9.	Select Review + Create, and then select Create.
![image](https://github.com/user-attachments/assets/df51a44f-ffcf-4418-9f58-f634af470c83)
 
10.	You do not need to wait for the resources to be created. Continue on to the next task.


## Task 2: Create a virtual machine in a different virtual network

In this task, you create a manufacturing services virtual network with a virtual machine.
1.	From the Azure portal, search for and navigate to Virtual Machines.
2.	From the virtual machines page, select Create then select Azure Virtual Machine.
3.	On the Basics tab, use the following information to complete the form, and then select Next: Disks >. For any setting not specified, leave the default value.
![image](https://github.com/user-attachments/assets/8958c14c-ea3a-49f8-b93a-37b4452fea30)
 
4.	On the Disks tab take the defaults and then select Next: Networking >.
5.	On the Networking tab, for Virtual network, select Create new.
6.	Use the following information to configure the virtual network, and then select Ok. If necessary, remove or replace the existing address range.
![image](https://github.com/user-attachments/assets/6d633fb3-324c-425e-bd6b-f178a64a650d)
 
7.	Select the Monitoring tab. For Boot Diagnostics, select Disable.
![image](https://github.com/user-attachments/assets/4745ea94-84f9-4434-88d7-8c96076fdb0b)
 
8.	Select Review + Create, and then select Create.
![image](https://github.com/user-attachments/assets/beb9075a-7867-4c89-ac16-a6386ff57eea)
 

## Task 3: Use Network Watcher to test the connection between virtual machines
In this task, you verify that resources in peered virtual networks can communicate with each other. Network Watcher will be used to test the connection. Before continuing, ensure both virtual machines have been deployed and are running.
![image](https://github.com/user-attachments/assets/452d3cd1-0c89-4765-a7ec-c128fe4fc3f5)
 

1.	From the Azure portal, search for and select Network Watcher.
2.	From Network Watcher, in the Network diagnostic tools menu, select Connection troubleshoot.
3.	Use the following information to complete the fields on the Connection troubleshoot page.
![image](https://github.com/user-attachments/assets/1590f6e0-5434-4ac0-961e-bb72f735f17f)
![image](https://github.com/user-attachments/assets/ec7ab934-ffe6-4358-9117-b5f16273ffa0)
 
 
4.	Select Run diagnostic tests.


## Task 4: Configure virtual network peerings between virtual networks
In this task, you create a virtual network peering to enable communications between resources in the virtual networks.
1.	In the Azure portal, select the CoreServicesVnet virtual network.
2.	In CoreServicesVnet, under Settings, select Peerings.
![image](https://github.com/user-attachments/assets/0338d321-fc2c-4113-8c61-8377036d61f2)
 
3.	On CoreServicesVnet	Peerings, select + Add. If not specified, take the default.
![image](https://github.com/user-attachments/assets/07629226-e5fb-4466-ac12-e7081823f84d)
 
1. In CoreServicesVnet	Peerings, verify that the CoreServicesVnet-to-ManufacturingVnet peering is listed. Refresh the page to ensure the Peering status is Connected.
![image](https://github.com/user-attachments/assets/3fac3df6-84c0-4c05-8e60-fbf02a96dac7)
 
2. Switch to the ManufacturingVnet and verify the ManufacturingVnet-to-CoreServicesVnet peering is listed. Ensure the Peering status is Connected. You may need to
Refresh the page.
![image](https://github.com/user-attachments/assets/f29c8010-506b-4b53-91ab-bdfdacdfdf41)
 

## Task 5: Use Azure PowerShell to test the connection between virtual machines

In this task, you retest the connection between the virtual machines in different virtual networks.
Verify the private IP address of the CoreServicesVM

1.	From the Azure portal, search for and select the CoreServicesVM virtual machine.
2.	On the Overview blade, in the Networking section, record the Private IP address of the machine. You need this information to test the connection.
![image](https://github.com/user-attachments/assets/61184f88-b189-4a85-98db-638554d08542)
 
Test the connection to the CoreServicesVM from the ManufacturingVM.
1.	Switch to the ManufacturingVM virtual machine.
2.	In the Operations blade, select the Run command blade.
![image](https://github.com/user-attachments/assets/427ba2c6-6bd2-448f-ade4-4346e9898f0e)
 
3.	Select RunPowerShellScript and run the Test-NetConnection command. Be sure to use the private IP address of the CoreServicesVM.
4.	It may take a couple of minutes for the script to time out. The top of the page shows an informational message Script execution in progress.
5.	The test connection should succeed because peering has been configured. Your computer name and remote address in this graphic may be different.
![image](https://github.com/user-attachments/assets/0e0a7968-bab4-4a83-afa9-9e5bddb68099)
 

## Task 6: Create a custom route

In this task, you want to control network traffic between the perimeter subnet and the internal core services subnet. A virtual network appliance will be installed in the core services subnet and all traffic should be routed there.

1.	Search for select the CoreServicesVnet.
2.	Select Subnets and then + Create. Be sure to Save your changes.
![image](https://github.com/user-attachments/assets/99a07ded-dec9-4817-8792-5b4c7d8bdef4)
 
3.	In the Azure portal, search for and select Route tables, and then select Create.
![image](https://github.com/user-attachments/assets/4e36d951-6b47-42b3-bb57-93fb2ce73cbf)
 
4.	After the route table deploys, select Go to resource.
5.	Select Routes and then + Add. Create a route from the future NVA to the CoreServices virtual network.
![image](https://github.com/user-attachments/assets/a91432db-0e46-4f5e-8479-49d78410d21d)
![image](https://github.com/user-attachments/assets/d975c1ef-011f-4dc8-9c57-e287296e998c)
 
 
6.	Select + Add when the route is completed. The last thing to do is associate the route with the subnet.
7.	Select Subnets and then Associate. Complete the configuration.
![image](https://github.com/user-attachments/assets/23d77be8-a393-4b7e-a89b-4978f1eb3bf0)
![image](https://github.com/user-attachments/assets/e031e6a2-1ee7-4cba-9a78-4775f0417fbb)

  

Cleanup your resources
If you are working with your own subscription take a minute to delete the lab resources. This will ensure resources are freed up and cost is minimized. The easiest way to delete the lab resources is to delete the lab resource group.

•	Using Azure PowerShell, Remove-AzResourceGroup -Name resourceGroupName.
•	Using the CLI, az group delete --name resourceGroupName.
![image](https://github.com/user-attachments/assets/6790d199-cbaa-47aa-93b3-2966db317740)
![image](https://github.com/user-attachments/assets/e917f71b-8956-4cf5-b970-bf994e194aec)
 
 
 
