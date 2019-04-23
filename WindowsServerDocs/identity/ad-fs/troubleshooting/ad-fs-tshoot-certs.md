---
title: AD FS-Problembehandlung – Zertifikate
description: Dieses Dokument beschreibt die typischen Zertifikatsprobleme.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 42fdce936bb4a6f25b456c4a96c7b99f650e6033
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860581"
---
# <a name="ad-fs-troubleshooting---certificates"></a>AD FS-Problembehandlung – Zertifikate
AD FS erfordert die folgenden Zertifikate, um ordnungsgemäß zu funktionieren.  Wenn diese nicht ordnungsgemäß konfiguriert oder eingerichtet haben, können Probleme auftreten.  

## <a name="required-certificates"></a>Erforderliche Zertifikate
AD FS erfordert die folgenden Zertifikate:



- **Verbundvertrauensstellung** – dies erfordert, dass entweder ein Zertifikat mit einem gegenseitig Internet vertrauenswürdigen Zertifizierungsstelle (Certificate Authority, CA) verkettet im vertrauenswürdigen Stammspeicher des Verbundserver, vertrauende Seite und Anspruchsanbieter-Vertrauensstellung vorhanden ist ein kreuzzertifizierungs-Entwurf wurde implementiert, in dem jede Seite die Stamm-ZS mit seinem Partner ausgetauscht wurde, oder selbstsignierten Zertifikate, die auf jeder Seite gegebenenfalls importiert wurden.
- **Token-signing** – jede Verbunddienst-Computer erfordert ein Token-signing Certificate.  Die Ansprüche Anbieter Tokensignaturzertifikat muss durch die vertrauende Seite Verbundserver vertrauenswürdig sein. Die relying Party Tokensignaturzertifikat muss von allen Anwendungen, die Token von der RP-Verbundserver empfangen, vertrauenswürdig sein.
- **Secure Sockets Layer (SSL)** – das SSL-Zertifikat für den Verbunddienst muss in einem vertrauenswürdigen Speicher auf dem Federation Server Proxy-Computer vorhanden sein und muss eine gültige Vertrauenskette einer vertrauenswürdigen Zertifizierungsstelle (Certificate Authority, CA)-Speicher.
- **Zertifikat der Sperrliste (CRL)** – für alle Zertifikate, die eine Zertifikatsperrliste veröffentlicht, die Zertifikatsperrliste muss auf allen Clients und Servern, die Zugriff auf das Zertifikat zugreifen kann.

Wenn alle oben genannten Schritte nicht ordnungsgemäß konfiguriert sind, funktioniert die AD FS nicht.

## <a name="common-things-to-check-with-certificates"></a>Allgemeine Überprüfungen mit Zertifikaten
Im folgenden finden eine Liste der Aufgaben, die auftreten können, und sollte überprüft werden, bei dem Versuch, ein Zertifikatsproblem zu beheben.

- Stellen Sie sicher, dass das Zertifikat vertrauenswürdig ist.
    - SSL-Zertifikate müssen von den Clients als vertrauenswürdig eingestuft werden
    - Token-Signaturzertifikate müssen die vertrauenden Seiten als vertrauenswürdig eingestuft werden
- Überprüfen der Vertrauenskette - jedes Zertifikat in der Kette muss gültig sein.
- Überprüfen Sie das Ablaufdatum des Zertifikats
- (Certificate Revocation List, CRL) Barrierefreiheit überprüfen
    - Stellen Sie sicher, dass die CDP-Feld wird aufgefüllt
    - Navigieren Sie manuell Sperrlisten-Verteilungspunkt
- Stellen Sie sicher, dass das Zertifikat nicht gesperrt wurde

## <a name="common-certificate-errors"></a>Allgemeine Zertifikatfehler
In der folgende Tabelle ist eine Liste von häufig auftretenden Fehlern und mögliche Ursachen.

|Ereignis|Ursache|Auflösung
|-----|-----|-----|
|Ereignis 249 – ein Zertifikat nicht im Zertifikatspeicher gefunden. Im Zertifikat-Rollover-Szenarien kann dies möglicherweise einen Fehler verursachen, wenn der Verbunddienst signieren oder entschlüsseln mit diesem Zertifikat wird.|Das betreffende Zertifikat ist nicht im lokalen Zertifikatspeicher vorhanden, oder das Dienstkonto besitzt keine Berechtigung zum privaten Schlüssel des Zertifikats.|Stellen Sie sicher, dass das Zertifikat installiert ist im Speicher LocalMAchine\My auf dem AD FS-Server. Stellen Sie sicher, dass das AD FS-Dienstkonto über Lesezugriff auf den privaten Schlüssel des Zertifikats hat.|
|Ereignis 315 - Fehler beim Versuch, die im Rahmen der Zertifikatvertrauenskette für das Signaturzertifikat Anspruchsanbieter-Vertrauensstellung zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatkette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder ist noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die Zertifikatsperrliste möglich ist.|
|Ereignis 316 - Fehler beim Versuch, die im Rahmen der Zertifikatvertrauenskette für die Vertrauensstellung der vertrauenden Seite Signaturzertifikat zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatkette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder ist noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die Zertifikatsperrliste möglich ist.|
|Ereignis 317 - Fehler beim Versuch, die im Rahmen der Zertifikatvertrauenskette für das Verschlüsselungszertifikat der vertrauenden Seite Partei Vertrauensstellung zu erstellen.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatkette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder ist noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die Zertifikatsperrliste möglich ist.|
|Im Rahmen der Zertifikatvertrauenskette für das Clientzertifikat entwickelt wurde, ist Event 319 - ein Fehler aufgetreten.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatkette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder ist noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die Zertifikatsperrliste möglich ist.|
|Ereignis 360 - Anforderung wurde versucht, ein Zertifikat Verbindungsendpunkt des Transport, aber die Anforderung enthielt kein Clientzertifikat.|Die Stamm-ZS, die das Clientzertifikat ausgestellt ist nicht vertrauenswürdig.</br></br>Das Clientzertifikat ist abgelaufen.</br></br>Das Client-Zertifikat ist selbstsigniert und ist nicht vertrauenswürdig.|Stellen Sie sicher, dass die Stamm-ZS, die das Clientzertifikat ausgestellt im vertrauenswürdigen Stammspeicher vorhanden ist.</br></br>Stellen Sie sicher, dass das Clientzertifikat nicht abgelaufen ist.</br></br>Wenn der Client-Zertifikat selbstsigniert ist, stellen Sie sicher, dass sie die Liste der vertrauenswürdigen Zertifikate hinzugefügt wurde, oder Ersetzen Sie das selbstsignierte Zertifikat, mit einem vertrauenswürdigen Zertifikat.|
|Ereignis 374 - Fehler beim Erstellen im Rahmen der Zertifikatvertrauenskette für den Anspruchsanbieter-Vertrauensstellung Verschlüsselungszertifikat.|Das Zertifikat wurde gesperrt.</br></br>Die Zertifikatkette kann nicht überprüft werden.</br></br>Das Zertifikat ist abgelaufen oder ist noch nicht gültig.|Stellen Sie sicher, dass das Zertifikat gültig und nicht widerrufen wurde.</br></br>Stellen Sie sicher, dass die Zertifikatsperrliste möglich ist.|
|Ereignis 381 - Fehler beim Versuch, die im Rahmen der Zertifikatvertrauenskette für Konfiguration Zertifikat zu erstellen.|Eines der Zertifikate für die Verwendung auf dem AD FS-Server konfiguriert ist abgelaufen oder gesperrt wurde.|Stellen Sie sicher, dass alle konfigurierten Zertifikate nicht widerrufen wurde, und nicht abgelaufen.|
|Ereignis 385 - ermittelt AD FS, ein oder mehrere Zertifikate in der AD FS-Konfigurationsdatenbank muss manuell aktualisiert werden.|Eines der Zertifikate für die Verwendung auf dem AD FS-Server konfiguriert ist abgelaufen oder seinem Ablaufdatum nähert.|Aktualisieren Sie das Zertifikat ist abgelaufen oder läuft in Kürze-auf-ab, mit einem anderen. (Wenn Sie selbstsignierte Zertifikate verwenden, und automatischer zertifikatrollover aktiviert ist, kann dieser Fehler ignoriert, da es automatisch behoben wird.)|
|Ereignis 387 - erkannt AD FS, dass mindestens eines der Zertifikate, die im Verbunddienst angegeben sind nicht für das Dienstkonto zugänglich sind, die von der AD FS-Windows-Dienst verwendet wird.|Das AD FS-Dienstkonto besitzt keine Leseberechtigungen für den privaten Schlüssel von einem oder mehreren konfigurierten Zertifikaten.|Stellen Sie sicher, dass das AD FS-Dienstkonto die Berechtigung für den privaten Schlüssel aller konfigurierten Zertifikate gelesen hat.|
|Ereignis 389 - erkannt AD FS, dass eine oder mehrere Ihrer Vertrauensstellungen benötigen die Zertifikate manuell aktualisiert werden, weil sie abgelaufen sind oder bald abläuft.|Einer der Ihre konfigurierte partnerzertifikate ist abgelaufen oder läuft bald ab. Dies kann entweder einer Anspruchsanbieter-Vertrauensstellung oder Vertrauensstellung einer vertrauenden Seite gilt.|Wenn Sie diese Vertrauensstellung manuell erstellt haben, aktualisieren Sie manuell die Zertifikatkonfiguration. Wenn Sie die Metadaten des Verbunds verwendet, um die Vertrauensstellung zu erstellen, wird das Zertifikat automatisch aktualisiert, sobald der Partner das Zertifikat aktualisiert.|




## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)
 