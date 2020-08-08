---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: Verbesserte Interoperabilität mit SAML 2.0
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d92859a7f8ae37f847a68dae9ca7fd0245308b6a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954226"
---
# <a name="improved-interoperability-with-saml-20"></a>Verbesserte Interoperabilität mit SAML 2.0




AD FS in Windows Server 2016 enthält zusätzliche SAML-Protokoll Unterstützung, einschließlich der Unterstützung für den Import von Vertrauens Stellungen basierend auf Metadaten, die mehrere Entitäten enthalten.  Dadurch kann AD FS für die Teilnahme an Verbünden wie der InCommon Federation und anderen Implementierungen konfiguriert werden, die dem eGov 2.0-Standard entsprechen.

Die neue Funktion basiert auf Gruppen Vertrauensstellungen der vertrauenden Seite oder Anspruchs Anbieter-Vertrauens Stellungen. Jede Gruppe ist ein Element vom Typ entitiesdescriptor (<MD: entitiesdescriptor>), wie im "eGov 2,0"-Profil angegeben, das ein oder mehrere EntityDescriptor-Elemente enthält.  Die Gruppen verfügen über allgemeine Autorisierungs Regeln, und alle anderen Eigenschaften können wie einzelne Vertrauensstellungs Objekte geändert werden.

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

## <a name="references"></a>References

Das Profil "eGov 2,0" finden Sie [hier.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)

Die SAML-Kern Spezifikation finden Sie [hier.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)


