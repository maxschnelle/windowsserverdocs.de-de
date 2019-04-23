---
title: AD FS-Problembehandlung – Fiddler
description: Dieses Dokument beschreibt, was Fiddler ist und das Installieren und konfigurieren Sie Fiddler, um AD FS-Anspruchsanbieter-Probleme zu beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 822300d0e4b6ae462a3c942e22530bbed5f93e86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865631"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS-Problembehandlung – Fiddler
Fiddler ist ein Tool, das zum Erfassen von HTTP/HTTPS-Webdatenverkehr verwendet werden kann.  Dieses Tool kann verwendet werden, bei der Problembehandlung bei der Ausstellung Schadensvorgang unterstützen.  Anhand des Datenverkehrs erhalten wir ein besseres Verständnis der, in denen die Interaktion Überwindung ist.  In diesem Dokument wird beschrieben, wie zum Installieren und Einrichten von Fiddler zur Erfassung von AD FS-Verkehr.  Ein Beispiel Fiddler-Ablaufverfolgung, die mit WS-Federation finden Sie unter [AD FS-Problembehandlung – Fiddler - WS-Verbund](ad-fs-tshoot-fiddler-ws-fed.md)

## <a name="download-and-install-fiddler"></a>Herunterladen und Installieren von Fiddler
Sie können Fiddler [hier](https://www.telerik.com/download/fiddler).  Nachdem Sie heruntergeladen haben fahren Sie fort, und installieren Sie es.

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>Konfigurieren Sie Fiddler zur Erfassung von AD FS-Verkehr
Um AD FS-Datenverkehr zu erfassen, müssen wir Fiddler zum Entschlüsseln der SSL-Datenverkehr zu konfigurieren. 

### <a name="configure-the-fiddler-ssl-certificate"></a>Konfigurieren Sie das Fiddler-SSL-Zertifikat
 Verwenden Sie das folgende Verfahren zum Einrichten von Fiddler, um SSL-Datenverkehr entschlüsseln.

1.  Öffnen von Fiddler
2.  Klicken Sie oben unter **Tools**Option **Fiddler-Optionen**.
3.  Klicken Sie auf der Registerkarte "HTTPS".
4.  Aktivieren Sie das Kontrollkästchen **Entschlüsseln von HTTPS-Datenverkehr** , und wählen Sie **von Browsern nur** aus der Dropdownliste aus.
5.  Aktivieren Sie das Kontrollkästchen **Server Zertifikatfehler ignoriert**.
6.  Klicken Sie auf **OK**.

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)