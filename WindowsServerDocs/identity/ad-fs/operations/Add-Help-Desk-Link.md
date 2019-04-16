---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: "Hinzufügen von Helpdesklinks"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d16cc0a75bfe636c29b44687b669e87f31b69ce
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="add-help-desk-link"></a>Hinzufügen von Helpdesklinks 

>Gilt für: Windows Server 2016, Windows Server2012 R2


## <a name="to-add-a-help-desk-link"></a>So fügen Sie eine Helpdesklinks hinzu  
Um helpdesklinks hinzufügen, die auf der Anmeldeseite angezeigt wird, verwenden Sie die folgenden Windows PowerShell-PowerShell-Cmdlet und die folgende Syntax.  

![Fügen Sie beim Helpdesk](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> Die `linkText`Parameter in diesem Cmdlet ist nicht erforderlich, es sei denn, Sie verwenden einen anderen Wert als den Standardwert handelt es sich *Hilfe*. Der Vorteil der Verwendung der Standardwert ist, dass sie für alle clientgebietsschemata lokalisiert sind. Nachdem die Seite angepasst ist, hat die Anpassung Vorrang vor; aus diesem Grund sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
