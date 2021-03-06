---
title: About images for Windows virtual machines | Microsoft Docs
description: Learn about how images are used with Windows virtual machines in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management

ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: cynthn

---
# About images for Windows virtual machines
> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For information about finding and using images in the Resource Manager model, see [here](virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../includes/virtual-machines-common-classic-about-images.md)]

## Working with images
You can use the Azure PowerShell module to manage the images available to your Azure subscription. You also can use the Azure classic portal for some image tasks, but the command line gives you more options.

* **Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images as well as those provided by Azure or partners. This means you might get a large list. The next examples show how to get a shorter list.
* **Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.
* **Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` this works by filtering the DataDiskConfiguration property, which only applies to VM Images. This example also filters the output to only the label and image name.
* **Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`
  >[Azure.Tip] The OSState parameter is required if you want to create a VM image, which includes data disks as well as the operating system disk. If you don’t use the parameter, the cmdlet creates an OS image. The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.
* **Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## Next Steps
You can also [create a Windows machine using the classic portal](virtual-machines-windows-classic-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

