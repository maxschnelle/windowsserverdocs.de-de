---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: "Hinzufügen eines Startseitenlinks"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb903c62e717e36099934e64e1c939a502f691a3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-home-link"></a>Hinzufügen eines Startseitenlinks 

>Gilt für: Windows Server 2016, Windows Server2012 R2

Zum Hinzufügen des Startseitenklinks, der auf der Anmeldeseite angezeigt wird, verwenden Sie die folgenden Windows PowerShell-Cmdlet und die folgende Syntax. 


![Hinzufügen eines Startseitenlinks](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> Die `linkText`Parameter in diesem Cmdlet ist nicht erforderlich, es sei denn, Sie verwenden einen anderen Wert als den Standardwert handelt es sich *Home*. Der Vorteil der Verwendung der Standardwert ist, dass sie für alle clientgebietsschemata lokalisiert sind. Nachdem die Anmeldeseite angepasst ist, hat die Anpassung Vorrang vor; aus diesem Grund sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
