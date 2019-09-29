---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Hinzufügen eines Startseitenlinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5f1fad340629304fdf960139be05b8dbc2690e0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407774"
---
# <a name="add-home-link"></a>Hinzufügen eines Startseitenlinks 

Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um den Link "Home" hinzuzufügen, der auf der Seite "Sign @ no__t-0in" angezeigt wird. 


![Start Link hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Home*verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. Nachdem die Seite Sign @ no__t-0in angepasst ist, hat die Anpassung Vorrang. Daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
