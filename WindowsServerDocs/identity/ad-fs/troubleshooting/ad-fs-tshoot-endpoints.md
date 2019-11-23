---
title: AD FS Problembehandlung-AD FS Endpunkte
description: In diesem Dokument wird beschrieben, wie AD FS Endpunkte behoben werden.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 807b5c5de14bf6a43419d0b9d2d3a4e6953d0075
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366224"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS Problembehandlung-AD FS Metadatenendpunkte
Endpunkte ermöglichen den Zugriff auf die Verbund Serverfunktionen von AD FS, z. b. das Veröffentlichen von Verbund Metadaten.  Um zu überprüfen, ob der AD FS Server auf Webanforderungen antwortet, können wir die verschiedenen Endpunkte überprüfen.


## <a name="federation-metadata-test"></a>Verbund Metadaten-Test
Passiver Verbund bezieht sich auf Szenarien, in denen Ihr Browser auf die AD FS Anmeldeseite umgeleitet wird.  Durch Testen des Metadatenendpunkts können Sie feststellen, ob der AD FS Server in diesen passiven Szenarien auf Webanforderungen antwortet.  Verwenden Sie das folgende Verfahren, um den Endpunkt zu testen.

1.  Navigieren Sie in einem Webbrowser zu Ihrem AD FS Verbund-Metadatenendpunkt.  Beispiel: https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Die XML-Datei sollte lokal auf Ihren Computer heruntergeladen werden.
3. Öffnen Sie die Datei, und stellen Sie sicher, dass Sie Informationen enthält, die der folgenden integrieren ähneln: ![passive](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS-MEX-Test (aktiver Test)
Bei WS-MetaDataExchange handelt es sich um ein Webdienst Protokoll, das Teil der WS-Verbund-Roadmap ist.  Es wird eine SOAP-Nachricht verwendet, um Metadaten anzufordern.  Durch Testen des Endpunkts können Sie feststellen, ob der AD FS Server auf Webanforderungen für WS-MetaDataExchange antwortet.  Verwenden Sie das folgende Verfahren, um den Endpunkt zu testen.
1.  Navigieren Sie in einem Webbrowser zu Ihrem AD FS Verbund-Metadatenendpunkt.  Beispiel: https://sts.contoso.com/adfs/services/trust/mex
2. Die XML-Datei sollte automatisch im Browser angezeigt werden.  Dies sollte wie in der folgenden Abbildung aussehen:

![Aktiv](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)