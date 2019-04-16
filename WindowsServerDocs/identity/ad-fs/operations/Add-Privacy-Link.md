---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: "Hinzufügen eines Datenschutzlinks"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81a453b45693b8222bdfc0231885b506fdfcd2fc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-privacy-link"></a>Hinzufügen eines Datenschutzlinks 

>Gilt für: Windows Server 2016, Windows Server2012 R2

Zum Hinzufügen des Datenschutzklinks, der auf der Anmeldeseite angezeigt wird, verwenden Sie die folgenden Windows PowerShell-Cmdlet und die folgende Syntax.  

![Hinzufügen eines Datenschutzlinks](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> Die `linkText`Parameter in diesem Cmdlet ist nicht erforderlich, es sei denn, Sie verwenden einen anderen Wert als den Standardwert handelt es sich *Datenschutz*. Der Vorteil der Verwendung der Standardwert ist, dass die Seiten für alle clientgebietsschemata lokalisiert werden. Nachdem die Anmeldeseite angepasst ist, hat die Anpassung Vorrang vor; aus diesem Grund sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten Sie konfigurieren es mit einem Gebietsschema Country\ weniger zuerst, z.B. "En", bevor Sie Land und Region\ Gebietsschema, z.B. konfigurieren "En\-us".  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
