---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: Hinzufügen eines Helpdesklinks
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0aa57147ed2565db9cf8cde0addeb13432cb8856
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859403"
---
# <a name="add-help-desk-link"></a>Hinzufügen eines Helpdesklinks 


## <a name="to-add-a-help-desk-link"></a>So fügen Sie einen Helpdesk-Link hinzu  
Zum Hinzufügen des helpdesklinks, der auf der Seite Sign\-in angezeigt wird, verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  

![Helpdesk hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> Der `linkText`-Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Help* verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. Nachdem die Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
