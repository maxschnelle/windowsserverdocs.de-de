---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: "Verbesserte Interoperabilität mit SAML 2.0"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4f55eaacec8ee0eb41e1980f1aa15c6256f8b979
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="improved-interoperability-with-saml-20"></a>Verbesserte Interoperabilität mit SAML 2.0

>Gilt für: Windows Server 2016

  
AD FS unter Windows Server 2016 enthält zusätzliche SAML-Protokoll unterstützt, u. a. die Unterstützung für den Import von Vertrauensstellungen, die basierend auf Metadaten, die mehrere Elemente enthält.  Dadurch können Sie die Konfiguration von AD FS zur Teilnahme an Gewerkschaftsbund wie InCommon Verbundserver und anderen Implementierungen, die die eGov 2.0-Standard entsprechen.   
  
Die neue Funktion basiert auf Gruppen von der vertrauenden Seite oder Anspruchsanbieter-Vertrauensstellungen. Jede Gruppe ist ein Element EntitiesDescriptor (< Md:EntitiesDescriptor >), wie in der eGov 2.0 Profil angegeben, die einem oder mehreren EntityDescriptor Elemente enthält.  Die Gruppen haben häufig Autorisierungsregeln und alle anderen Eigenschaften können geändert werden, wie einzelne vertrauensstellungsobjekten.  
  
Sobald die Vertrauensstellung Gruppen in AD FS importiert wurden, die Vertrauensstellungen automatisch von AD FS als Gruppe auf Grundlage der Metadaten aktualisiert.  
  
Aktivieren diese Szenarien ist ganz einfach über die neue PowerShell-Cmdlets, die auf Objekte hinzufügen und Entfernen von AdfsClaimsProviderTrustsGroup und AdfsRelyingPartyTrustsGroup. Dies kann mit einer Metadaten-URL oder eine Datei, wie in den folgenden Beispielen gezeigt.  
  
Darüber hinaus wurde AD FS 2016 Unterstützung für den bereichsdefinierenden-Parameter, wie in Abschnitt 3.4.1.2 der SAML-Core-Spezifikation beschrieben. Dieses Element ermöglicht der vertrauenden Seite Parteien, geben Sie einen oder mehrere Identitätsanbietern für eine Authentifizierung anfordern.  
  
## <a name="examples"></a>Beispiele für  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>Verweise  
  
Das Profil eGov 2.0 finden Sie [hier.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
Die SAML-Core-Spezifikation finden Sie [hier.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


