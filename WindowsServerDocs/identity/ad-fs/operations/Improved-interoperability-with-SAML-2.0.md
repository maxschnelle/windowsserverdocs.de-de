---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: Verbesserte Interoperabilität mit SAML 2.0
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d72636d77fe3240caab66dcab8657225d291bec6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407543"
---
# <a name="improved-interoperability-with-saml-20"></a>Verbesserte Interoperabilität mit SAML 2.0



  
AD FS in Windows Server 2016 enthält zusätzliche SAML-Protokoll Unterstützung, einschließlich der Unterstützung für den Import von Vertrauens Stellungen basierend auf Metadaten, die mehrere Entitäten enthalten.  Dies ermöglicht es Ihnen, AD FS für die Teilnahme an Verbund-, wie z. b. einem gemeinsamen Verbund und anderen Implementierungen zu konfigurieren, die mit dem eGov 2,0-Standard   
  
Die neue Funktion basiert auf Gruppen Vertrauensstellungen der vertrauenden Seite oder Anspruchs Anbieter-Vertrauens Stellungen. Jede Gruppe ist ein Element vom Typ entitiesdescriptor (< MD: entitiesdescriptor >), wie im "eGov 2,0"-Profil angegeben, das ein oder mehrere EntityDescriptor-Elemente enthält.  Die Gruppen verfügen über allgemeine Autorisierungs Regeln, und alle anderen Eigenschaften können wie einzelne Vertrauensstellungs Objekte geändert werden.  
  
Nachdem die Vertrauens Gruppen in AD FS importiert wurden, aktualisiert AD FS die Vertrauens Stellungen automatisch als Gruppe basierend auf dem Metadatendokument.  
  
Die Aktivierung dieser Szenarios ist so einfach wie die Verwendung der neuen PowerShell-Cmdlets, die adfsclaimsprovidertrustsgroup-und adfsrelyingpartytrustsgroup-Objekte hinzufügen und daraus entfernen. Dies kann mithilfe einer Metadaten-URL oder einer Datei erfolgen, wie in den folgenden Beispielen gezeigt.  
  
Außerdem verfügt AD FS 2016 über Unterstützung für den Bereichs Parameter, wie in der SAML-Kern Spezifikation, Abschnitt 3.4.1.2, beschrieben. Dieses Element ermöglicht es den vertrauenden Seiten, mindestens einen Identitäts Anbieter für eine Authentifizierungsanforderung anzugeben.  
  
## <a name="examples"></a>Beispiele  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>Verweise  
  
Das Profil "eGov 2,0" finden Sie [hier.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
Die SAML-Kern Spezifikation finden Sie [hier.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


