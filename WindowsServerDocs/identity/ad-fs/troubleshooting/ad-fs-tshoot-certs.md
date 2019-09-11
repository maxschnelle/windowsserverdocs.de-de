---
title: 'AD FS Problembehandlung: Zertifikate'
description: In diesem Dokument werden typische Zertifikat Probleme beschrieben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cee87ce864e333b98e92fa64e939f2ead7edc156
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869189"
---
# <a name="ad-fs-troubleshooting---certificates"></a>AD FS Problembehandlung: Zertifikate
AD FS erfordert die folgenden Zertifikate, um ordnungsgemäß zu funktionieren.  Wenn eine dieser Einstellungen nicht eingerichtet oder ordnungsgemäß konfiguriert wurde, können Probleme auftreten.  

## <a name="required-certificates"></a>Erforderliche Zertifikate
AD FS erfordert die folgenden Zertifikate:



- Verbund **Vertrauensstellung** – dies erfordert, dass entweder ein Zertifikat, das mit einer gegenseitig vertrauenswürdigen Internet-Stamm Zertifizierungsstelle (ca) verkettet ist, im vertrauenswürdigen Stamm Speicher des Anspruchs Anbieters und der Verbund Server der vertrauenden Seite vorhanden ist. der Entwurf der Kreuz Zertifizierung wurde implementiert, wobei jede Seite die Stamm Zertifizierungsstelle mit Ihrem Partner ausgetauscht hat, oder selbst signierte Zertifikate, die ggf. auf jeder Seite importiert wurden.
- **Tokensignierung** – für jeden Verbunddienst Computer ist ein Tokensignaturzertifikat erforderlich.  Das Tokensignaturzertifikat des Anspruchs Anbieters muss vom Verbund Server der vertrauenden Seite als vertrauenswürdig eingestuft werden. Das Tokensignaturzertifikat der vertrauenden Seite muss von allen Anwendungen als vertrauenswürdig eingestuft werden, die Token vom RP-Verbund Server empfangen.
- **Secure Sockets Layer (SSL)** – das SSL-Zertifikat für die Verbunddienst muss in einem vertrauenswürdigen Speicher auf dem Verbund Server Proxy-Computer vorhanden sein und über eine gültige Kette zu einem Speicher der vertrauenswürdigen Zertifizierungsstelle (ca) verfügen.
- **Zertifikat Sperr Liste (CRL)** – für alle Zertifikate, die eine Zertifikat Sperr Liste veröffentlicht haben, muss für alle Clients und Server, die auf das Zertifikat zugreifen müssen, der Zugriff auf die CRL möglich sein.

Wenn eine der oben genannten nicht ordnungsgemäß konfiguriert ist, funktionieren AD FS nicht.

## <a name="common-things-to-check-with-certificates"></a>Allgemeine Dinge, die mit Zertifikaten überprüft werden müssen
Im folgenden finden Sie eine Liste der Dinge, die auftreten können und überprüft werden sollten, wenn Sie versuchen, ein Zertifikat Problem zu beheben.

- Stellen Sie sicher, dass das Zertifikat vertrauenswürdig ist.
    - SSL-Zertifikate müssen von den Clients als vertrauenswürdig eingestuft werden.
    - Tokensignaturzertifikate müssen von den vertrauenden Seiten als vertrauenswürdig eingestuft werden
- Überprüfen Sie die Vertrauenskette. jedes Zertifikat in der Kette muss gültig sein.
- Überprüfen des Ablaufdatums für das Zertifikat
- Überprüfen des Zugriffs auf die Zertifikat Sperr Liste (CRL)
    - Stellen Sie sicher, dass das CDP-Feld aufgefüllt ist
    - Manuelles Navigieren zum CDP
- Stellen Sie sicher, dass das Zertifikat nicht widerrufen wurde.

## <a name="common-certificate-errors"></a>Allgemeine Zertifikat Fehler
In der folgenden Tabelle sind häufige Fehler und mögliche Ursachen aufgeführt.

|event|Ursache|Auflösung
|-----|-----|-----|
|Ereignis 249: im Zertifikat Speicher wurde kein Zertifikat gefunden. In Szenarios für den zertifikatrol Lover kann dies möglicherweise zu einem Fehler führen, wenn die Verbunddienst mit diesem Zertifikat signiert oder entschlüsselt wird.|Das betreffende Zertifikat ist nicht im lokalen Zertifikat Speicher vorhanden, oder das Dienst Konto verfügt nicht über die Berechtigung für den privaten Schlüssel des Zertifikats.|Stellen Sie sicher, dass das Zertifikat im Speicher LocalMachine\MY auf dem AD FS Server installiert ist. Stellen Sie sicher, dass das AD FS-Dienst Konto über Lesezugriff auf den privaten Schlüssel des Zertifikats verfügt.|
|Ereignis 315: Fehler beim Versuch, die Zertifikat Kette für das Anspruchs Anbieter-Vertrauensstellungs Zertifikat zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatskette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig ist und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die CRL zugänglich ist.|
|Ereignis 316: Fehler beim Versuch, die Zertifikat Kette für das Signaturzertifikat der vertrauenden Seite zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatskette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig ist und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die CRL zugänglich ist.|
|Ereignis 317: Fehler beim Versuch, die Zertifikat Kette für das Verschlüsselungs Zertifikat der vertrauenden Seite zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatskette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig ist und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die CRL zugänglich ist.|
|Ereignis 319: Fehler beim Erstellen der Zertifikat Kette für das Client Zertifikat.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatskette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig ist und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die CRL zugänglich ist.|
|Ereignis 360: an einen Zertifikat Transport Endpunkt wurde eine Anforderung gerichtet, aber die Anforderung enthielt kein Client Zertifikat.|Die Stamm Zertifizierungsstelle, die das Client Zertifikat ausgestellt hat, ist nicht vertrauenswürdig.</br></br>Das Client Zertifikat ist abgelaufen.</br></br>Das Client Zertifikat ist selbst signiert und nicht vertrauenswürdig.|Stellen Sie sicher, dass die Stamm Zertifizierungsstelle, die das Client Zertifikat ausgestellt hat, im vertrauenswürdigen Stamm Speicher vorhanden ist.</br></br>Stellen Sie sicher, dass das Client Zertifikat nicht abgelaufen ist.</br></br>Wenn das Client Zertifikat selbst signiert ist, stellen Sie sicher, dass es der Liste der vertrauenswürdigen Zertifikate hinzugefügt wurde, oder ersetzen Sie das selbst signierte Zertifikat durch ein vertrauenswürdiges Zertifikat.|
|Ereignis 374: Fehler beim Aufbau der Zertifikat Kette für das Verschlüsselungs Zertifikat der Anspruchs Anbieter Vertrauensstellung.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatskette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig ist und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die CRL zugänglich ist.|
|Ereignis 381: Fehler beim Versuch, die Zertifikat Kette für das Konfigurations Zertifikat zu erstellen.|Eines der Zertifikate, die für die Verwendung auf dem AD FS-Server konfiguriert sind, ist abgelaufen oder wurde widerrufen.|Stellen Sie sicher, dass alle konfigurierten Zertifikate nicht gesperrt und nicht abgelaufen sind.|
|Ereignis 385-AD FS erkannt, dass mindestens ein Zertifikat in der AD FS Konfigurationsdatenbank manuell aktualisiert werden muss.|Eines der Zertifikate, die für die Verwendung auf dem AD FS-Server konfiguriert sind, ist abgelaufen oder nähert sich dem Ablaufdatum.|Aktualisieren Sie das abgelaufene oder bald ablaufende Zertifikat mit einer Ersetzung. (Wenn Sie selbst signierte Zertifikate verwenden und automatisches zertifikatrol Lover aktiviert ist, wird dieser Fehler möglicherweise ignoriert, da er sich selbst auflöst.)|
|Ereignis 387-AD FS erkannt, dass auf mindestens eines der Zertifikate, die in der Verbunddienst angegeben sind, für das Dienst Konto, das vom AD FS Windows-Dienst verwendet wird, nicht zugegriffen werden kann.|Das AD FS-Dienst Konto verfügt nicht über Leseberechtigungen für den privaten Schlüssel eines oder mehrerer konfigurierter Zertifikate.|Stellen Sie sicher, dass das AD FS-Dienst Konto über Leseberechtigung für den privaten Schlüssel aller konfigurierten Zertifikate verfügt.|
|Ereignis 389-AD FS erkannt, dass Ihre Zertifikate von mindestens einer Vertrauensstellung manuell aktualisiert werden müssen, da Sie abgelaufen sind oder bald ablaufen.|Eines der konfigurierten Partner Zertifikate ist abgelaufen oder läuft demnächst ab. Dies kann entweder für eine Anspruchs Anbieter-Vertrauensstellung oder für eine Vertrauensstellung der vertrauenden Seite gelten.|Wenn Sie diese Vertrauensstellung manuell erstellt haben, aktualisieren Sie die Zertifikat Konfiguration manuell. Wenn Sie zum Erstellen der Vertrauensstellung Verbund Metadaten verwendet haben, wird das Zertifikat automatisch aktualisiert, sobald der Partner das Zertifikat aktualisiert.|




## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
 