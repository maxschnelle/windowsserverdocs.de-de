---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: Hinzufügen eines Helpdesklinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1673e6ee6357a9d59e8ac5891625d453bb434088
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358464"
---
# <a name="add-help-desk-link"></a>Hinzufügen eines Helpdesklinks 


## <a name="to-add-a-help-desk-link"></a>So fügen Sie einen Helpdesk-Link hinzu  
Zum Hinzufügen des helpdesklinks, der auf der Seite Sign\-in angezeigt wird, verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  

![Helpdesk hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Help*verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. Nachdem die Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
