---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: Hinzufügen eines Helpdesklinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb186c3ba5cfb3acb9bfd0c3139b09b992fb8863
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190210"
---
# <a name="add-help-desk-link"></a>Hinzufügen eines Helpdesklinks 


## <a name="to-add-a-help-desk-link"></a>Hinzufügen einer Helpdesklinks  
Helpdesklinks hinzufügen, die auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  

![Fügen Sie beim Helpdesk](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Help*verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. Nachdem die Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.  


## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
