---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Hinzufügen eines Startseitenlinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb903c62e717e36099934e64e1c939a502f691a3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823011"
---
# <a name="add-home-link"></a>Hinzufügen eines Startseitenlinks 

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Zum Hinzufügen des startseitenklinks, der auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax. 


![Hinzufügen eines startseitenlinks](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Home*verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. nach der Anmeldefunktion\-Seite wird angepasst, die Anpassung Vorrang, daher sollten Sie für alle Sprachen, die Sie unterstützen möchten anpassen.

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
