---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: Hinzufügen eines Datenschutzlinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cd559e38c38e96d1417257fe7d6ff8ccfa180c6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358420"
---
# <a name="add-privacy-link"></a>Hinzufügen eines Datenschutzlinks 


Verwenden Sie zum Hinzufügen des Datenschutz Links, der auf der Seite Sign\-in angezeigt wird, das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  

![Datenschutz Link hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Privacy*verwenden. Der Vorteil des Standardwerts ist, dass die Seiten für alle Clientgebietsschemata lokalisiert sind. Nachdem die Seite Sign\-in angepasst ist, hat die Anpassung Vorrang. Daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten Sie diese zunächst mit einem Land\-weniger Gebiets Schema konfigurieren, z. b. "en", bevor Sie Land und Region\-bestimmtes Gebiets Schema konfigurieren, wie z. b. "en\-US".  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
