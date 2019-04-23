---
title: Überprüfen der Konfiguration nach der NPS-Änderungen
description: Sie können in diesem Thema verwenden, um Netzwerkrichtlinienserver für Windows Server 2016-Konfiguration zu überprüfen, nachdem eine IP-Adresse oder den Namen ändern, an den Server.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 144e414e32d413e4863b90ada671753155bc96d7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880671"
---
# <a name="verify-configuration-after-nps-changes"></a>Überprüfen der Konfiguration nach der NPS-Änderungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um NPS-Konfiguration zu überprüfen, nachdem eine IP-Adresse oder den Namen ändern, an den Server.

## <a name="verify-configuration-after-an-nps-ip-address-change"></a>Überprüfen der Konfiguration nach der eine Änderung der NPS-IP-Adresse

Es gibt möglicherweise Situationen, in denen Sie so ändern Sie die IP-Adresse eines NPS oder Proxy verwenden, z. B. Wenn Sie den Server mit einem anderen IP-Subnetz verschieben müssen. 

Wenn Sie eine NPS oder Proxy-IP-Adresse ändern, ist es erforderlich, um Teile der NPS-Bereitstellung neu zu konfigurieren. 

Verwenden Sie die folgenden allgemeinen Richtlinien zur Unterstützung beim sicherstellen, dass eine Änderung der IP-Adresse nicht Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführung in Ihrem Netzwerk für NPS RADIUS-Server und RADIUS-Proxyserver unterbrochen.

Sie müssen ein Mitglied sein **Administratoren**, oder äquivalent, um diese Verfahren ausführen.

### <a name="to-verify-configuration-after-an-nps-ip-address-change"></a>So überprüfen die Konfiguration nach der eine Änderung des NPS IP-Adresse

1. Konfigurieren Sie alle RADIUS-Clients, z. B. drahtlose Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS.

2. Wenn NPS ein Mitglied einer remote-RADIUS-Servergruppe ist, konfigurieren Sie die NPS-Proxy mit der neuen IP-Adresse des NPS.

3. Wenn Sie den NPS zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Konnektivität zwischen dem Computer mit SQL Server und Netzwerkrichtlinienserver weiterhin ordnungsgemäß arbeitet.

4. Wenn Sie IPsec zum Sichern von RADIUS-Datenverkehr zwischen den NPS und ein NPS-Proxy oder anderen Servern oder Geräten bereitgestellt haben, konfigurieren Sie die IPsec-Richtlinie oder die Verbindungssicherheitsregel in der Windows-Firewall mit erweiterter Sicherheit so verwenden Sie die neue IP-Adresse des NPS aus.

5. Wenn der NPS mehrfach vernetzt ist, und Sie den Server zum Binden an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie NPS-Port-Einstellungen mit der neuen IP-Adresse neu.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>So überprüfen die Konfiguration nach einem NPS-Proxy-IP-Adresse ändert

1. Konfigurieren Sie alle RADIUS-Clients, z. B. drahtlose Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS-Proxys.

2. Wenn der NPS-Proxy mehrfach vernetzt ist, und Sie den Proxy zum Binden an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie NPS-Port-Einstellungen mit der neuen IP-Adresse neu.

3. Konfigurieren Sie alle Mitglieder der alle remote-RADIUS-Servergruppen mit IP-Adresse des Proxyservers ein. Zur Ausführung dieser Aufgabe ein, auf jeden NPS, die die NPS-Proxy, der als RADIUS-Client konfiguriert wurde:

    a. Doppelklicken Sie auf **NPS (lokal)**, doppelklicken Sie auf **RADIUS-Clients und Servern**, klicken Sie auf **RADIUS-Clients**, und doppelklicken Sie dann im Detailbereich auf den RADIUS-Client, die Sie ändern möchten.

    b. In der RADIUS-Client **Eigenschaften**im **Adresse \(IP-Adresse oder DNS-\)**, geben Sie die neue IP-Adresse des NPS-Proxys.

4. Wenn Sie die NPS-Proxy zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Konnektivität zwischen dem Computer mit SQL Server und dem NPS-Proxy weiterhin ordnungsgemäß arbeitet.

## <a name="verify-configuration-after-renaming-an-nps"></a>Überprüfen der Konfiguration nach dem Umbenennen einer NPS

Wenn Sie zum Ändern des Namens eines NPS oder Proxy verwenden, z. B. Wenn Sie die Benennungskonventionen für Ihre Server Umgestalten müssen möglicherweise Situationen vor.

Wenn Sie einen NPS oder Proxy-Namen ändern, ist es erforderlich, um Teile der NPS-Bereitstellung neu zu konfigurieren. 

Verwenden Sie die folgenden allgemeinen Richtlinien zur Unterstützung beim sicherstellen, dass es sich bei eine Änderung des Servernamens Netzwerkzugriffsauthentifizierung, Autorisierung und Kontoführung nicht unterbrochen wird.

Sie müssen ein Mitglied sein **Administratoren**, oder äquivalent, um dieses Verfahren auszuführen.

### <a name="to-verify-configuration-after-an-nps-or-proxy-name-change"></a>So überprüfen die Konfiguration nach einer Änderung des NPS oder einem Proxyserver

1. Wenn der NPS ein Mitglied einer remote-RADIUS-Servergruppe ist aus, und die Gruppe mit Computernamen anstelle von IP-Adressen konfiguriert ist, konfigurieren Sie die remote-RADIUS-Servergruppe mit dem neuen NPS-Namen.

2. Wenn zertifikatbasierte Authentifizierungsmethoden an den NPS bereitgestellt werden, erklärt das Serverzertifikat für die Namensänderung ungültig. Sie können ein neues Zertifikat anfordern, vom Administrator Zertifizierungsstelle (CA) oder, wenn der Computer auf einem Domänenmitgliedscomputer und Zertifikate automatisch registrieren, um Mitglieder der Domäne ist, können Sie mit der Aktualisieren der Gruppenrichtlinie, um ein neues Zertifikat über die automatische Registrierung zu erhalten . So aktualisieren Sie die Gruppenrichtlinie:

    a. Öffnen Sie die Befehlszeile oder Windows PowerShell.

    b. Geben Sie **gpupdate** ein, und drücken Sie dann die EINGABETASTE.


3. Nachdem Sie ein neues Serverzertifikat verfügen, fordern Sie, dass der ZS-Administrator das alte Zertifikat widerrufen. 

     Nachdem das alte Zertifikat widerrufen wurde, weiterhin NPS verwenden, bis das alte Zertifikat läuft ab. Standardmäßig bleibt das alte Zertifikat für einen maximalen Zeitraum von einer Woche 10 Stunden gültig. Dieser Zeitraum möglicherweise variieren, je nachdem, ob der Ablauf des Windows-Verwaltungsinstrumentation (Certificate Revocation List, CRL) und der Ablauf der Zeit des Transport Layer Security (TLS)-Cache die Standardeinstellungen geändert wurden. Der Ablauf des Standard-Zertifikatsperrliste ist eine Woche. Der Standardwert TLS Zwischenspeichern Mal, wenn 10 Stunden wird. 

     Wenn Sie NPS, um sofort mit der Verwendung des neuen Zertifikats konfigurieren möchten, können jedoch Sie manuell Netzwerkrichtlinien mit dem neuen Zertifikat konfigurieren.

4. Nachdem das alte Zertifikat abgelaufen ist, beginnt NPS automatisch das neue Zertifikat verwendet. 

5. Wenn Sie den NPS zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Konnektivität zwischen dem Computer mit SQL Server und Netzwerkrichtlinienserver weiterhin ordnungsgemäß arbeitet.

