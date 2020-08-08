---
title: 'AD FS Problembehandlung: "fddler"'
description: In diesem Dokument wird beschrieben, was von "fddler" ist, und wie Sie "fddler" installieren und konfigurieren, um Probleme mit der AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.openlocfilehash: e631d9b1dd93b9f3eb3d224fa5e2007e3661e21c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972027"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS Problembehandlung: "fddler"
"Fddler" ist ein Tool, das zum Erfassen von HTTP/HTTPS-Webdatenverkehr verwendet werden kann.  Dieses Tool kann verwendet werden, um die Problembehandlung bei der Anspruchs Ausstellung zu unterstützen.  Durch die Betrachtung des Datenverkehrs können Sie besser verstehen, wo die Interaktion unterteilt ist.  In diesem Dokument wird beschrieben, wie Sie die Installation von und Setup für den Datenverkehr AD FS.  Ein Beispiel für die Verwendung von "fddler" mit dem WS-Verbund finden Sie unter [AD FS Troubleshooting-fddler-WS-Federation](ad-fs-tshoot-fiddler-ws-fed.md) .

## <a name="download-and-install-fiddler"></a>Herunterladen und Installieren von "fddler"
Sie können "fddler" [hier](https://www.telerik.com/download/fiddler)herunterladen.  Nachdem Sie Sie heruntergeladen haben, installieren Sie Sie.

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>Konfigurieren von "fddler" zum Erfassen AD FS Datenverkehrs
Um AD FS Datenverkehr zu erfassen, müssen wir "fddler" zum Entschlüsseln von SSL-Datenverkehr konfigurieren.

### <a name="configure-the-fiddler-ssl-certificate"></a>Konfigurieren des SSL-Zertifikats von "fddler"
 Verwenden Sie das folgende Verfahren, um den-Setup-Assistenten zum Entschlüsseln von SSL-Datenverkehr einzurichten.

1.  Öffnen Sie Fiddler.
2.  Wählen Sie im oberen Bereich unter Extras die **Option Optionen**für das options **Werk**aus.
3.  Klicken Sie auf die Registerkarte HTTPS.
4.  Aktivieren Sie den **HTTP-Datenverkehr entschlüsseln** , und wählen Sie aus der Dropdown-Dropdown-Option **nur aus Browsern aus** .
5.  Aktivieren Sie das Kontrollkästchen **Serverzertifikat Fehler ignorieren**.
6.  Klicken Sie auf **OK**.

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)