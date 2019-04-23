---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: Hinzufügen eines Datenschutzlinks
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81a453b45693b8222bdfc0231885b506fdfcd2fc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836801"
---
# <a name="add-privacy-link"></a>Hinzufügen eines Datenschutzlinks 

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Zum Hinzufügen des datenschutzklinks, der auf die Anmeldeseite angezeigt wird\-auf der Seite verwenden Sie die folgenden Windows PowerShell-Cmdlets und Syntax.  

![Hinzufügen eines datenschutzlinks](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> Der `linkText` -Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Privacy*verwenden. Der Vorteil des Standardwerts ist, dass die Seiten für alle Clientgebietsschemata lokalisiert sind. nach der Anmeldefunktion\-Seite wird angepasst, die Anpassung Vorrang, daher sollten Sie für alle Sprachen, die Sie unterstützen möchten anpassen. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten Sie es konfigurieren, mit einem Land\-weniger Gebietsschema erste, z. B. "En", bevor Sie Land und Region konfigurieren\-spezifische Gebietsschema, z. B. "En\-uns".  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
