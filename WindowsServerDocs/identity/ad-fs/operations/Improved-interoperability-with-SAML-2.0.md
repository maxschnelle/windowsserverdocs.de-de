---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: Verbesserte Interoperabilität mit SAML 2.0
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4148614ba35ce29f567edb08b94e115d3f9152e9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189101"
---
# <a name="improved-interoperability-with-saml-20"></a>Verbesserte Interoperabilität mit SAML 2.0



  
AD FS unter Windows Server 2016 enthält zusätzliche SAML-Protokoll-Unterstützung, einschließlich Unterstützung für das Importieren von Vertrauensstellungen, die basierend auf Metadaten, die mehrere Entitäten enthält.  Dadurch können Sie zum Konfigurieren von AD FS für die Teilnahme an Gewerkschaftsbund wie z. B. InCommon Verbund und anderen Implementierungen, die eGov 2.0-Standards entsprechen.   
  
Die neue Funktion basiert auf Gruppen von vertrauende Seite oder die Anspruchsanbieter-Vertrauensstellungen. Jede Gruppe ist ein EntitiesDescriptor (< Md:EntitiesDescriptor >)-Element in der eGov 2.0-Profil angegeben, die eine oder mehrere EntityDescriptor-Elemente enthält.  Die Gruppen enthalten allgemeine Autorisierungsregeln aus, und alle anderen Eigenschaften können geändert werden, wie einzelne Trust-Objekte.  
  
Sobald die Vertrauensstellung Gruppen in AD FS importiert wurden, die Vertrauensstellungen automatisch von AD FS als eine Gruppe basierend auf dem Dokument aktualisiert.  
  
Aktivieren diese Szenarien ist so einfach wie die Verwendung der neuen PowerShell-Cmdlets, die auf Objekte hinzufügen und Entfernen von AdfsClaimsProviderTrustsGroup und AdfsRelyingPartyTrustsGroup. Dies kann erfolgen mithilfe einer Metadaten-URL oder eine Datei, wie in den folgenden Beispielen gezeigt.  
  
Darüber hinaus hat es sich bei AD FS 2016 um Unterstützung für den Bereichsparameter, wie in der SAML-Core-Spezifikation, Abschnitt 3.4.1.2 beschrieben. Dieses Element ermöglicht der vertrauenden Seite Parteien angeben oder weitere Identitätsanbieter für eine Authentifizierung anzufordern.  
  
## <a name="examples"></a>Beispiele  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>Verweise  
  
Das Profil eGov 2.0 finden Sie [hier.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
Der SAML-hauptspezifikation finden [hier.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


