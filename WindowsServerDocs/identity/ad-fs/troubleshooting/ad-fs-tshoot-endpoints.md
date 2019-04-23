---
title: AD FS-Problembehandlung – AD FS-Endpunkte
description: Dieses Dokument beschreibt die Problembehandlung für AD FS-Endpunkte
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13b830c0317341280bd87499e3abd8dcd1a33fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857561"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS-Problembehandlung – AD FS-Endpunkte
Endpunkte bieten Zugriff auf die Verbund-Funktionen von AD FS, z. B. veröffentlichen Metadaten des Verbunds.  Um sicherzustellen, dass AD FS-Servers auf webanforderungen geantwortet wird, können wir die verschiedenen Endpunkte überprüfen.


## <a name="federation-metadata-test"></a>Verbund-Metadaten-test
Passiven Verbund bezieht sich auf Szenarien, in dem Browser erneut an die AD FS-Anmeldeseite geleitet wird.  Testen des Metadaten-Endpunkts können wir feststellen, ob AD FS-Servers auf webanforderungen in diesen Szenarien passiven reagiert.  Verwenden Sie das folgende Verfahren, um den Endpunkt zu testen.

1.  Mithilfe eines Webbrowsers, navigieren Sie zu der AD FS-Verbund-Metadatenendpunkt.  Zum Beispiel:  https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Die XML-Datei muss lokal auf Ihren Computer herunterzuladen.
3. Öffnen Sie sie aus, und stellen Sie sicher, dass sie die Informationen ähnlich wie die folgenden Informationen enthält: ![Passive](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS-MEX-Test (Active-Test)
WS-MetaDataExchange ist ein Webprotokoll-Dienste und ist Teil der Roadmap für die WS-Verbund.  Eine SOAP-Nachricht verwendet zum Anfordern von Metadaten.  Testen Sie den Endpunkt können wir feststellen, ob der AD FS-Server für die WS-MetaDataExchange auf webanforderungen geantwortet wird.  Verwenden Sie das folgende Verfahren, um den Endpunkt zu testen.
1.  Mithilfe eines Webbrowsers, navigieren Sie zu der AD FS-Verbund-Metadatenendpunkt.  Zum Beispiel:  https://sts.contoso.com/adfs/services/trust/mex
2. Die XML-Datei sollte im Browser automatisch angezeigt werden.  Es sollte wie folgt aussehen:

![Aktiv](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)