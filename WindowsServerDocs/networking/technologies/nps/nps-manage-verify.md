---
title: Überprüfen der Konfiguration nach NPS-Serveränderungen
description: In diesem Thema können Sie um Windows Server2016 Network Policy Server-Konfiguration zu überprüfen, nachdem eine IP-Adresse oder den Namen ändern, mit dem Server.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f4d7e003fb037d18c5e5f2036a419383885eaf9e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="verify-configuration-after-nps-server-changes"></a>Überprüfen der Konfiguration nach NPS-Serveränderungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema verwenden, um NPS-Serverkonfiguration zu überprüfen, nachdem eine IP-Adresse oder den Namen ändern, mit dem Server.

## <a name="verify-configuration-after-an-nps-server-ip-address-change"></a>Überprüfen der Konfiguration nach einer NPS-Server IP-Adresse ändern

Möglicherweise Situationen, in denen Sie die IP-Adresse eines NPS-Server oder Proxy, z.B. Wenn Sie den Server zu einem anderen IP-Subnetz verschieben ändern müssen. 

Wenn Sie einen NPS-Server oder Proxy-IP-Adresse ändern, ist es erforderlich, um Teile der NPS-Bereitstellung neu konfigurieren. 

Verwenden Sie die folgenden Richtlinien, um zu überprüfen, dass eine Änderung der IP-Adresse nicht Netzwerkzugriffsauthentifizierung, Autorisierung oder Kontoführung auf Ihr Netzwerk nach NPS RADIUS-Server und RADIUS-Proxyserver unterbrochen.

Sie müssen ein Mitglied sein **Administratoren**, oder die entsprechende Berechtigung zum Ausführen dieser Verfahren.

### <a name="to-verify-configuration-after-an-nps-server-ip-address-change"></a>So überprüfen die Konfiguration nach einem NPS-Server IP-Adresse ändern

1. Konfigurieren Sie alle RADIUS-Clients, z.B. drahtlose Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS-Servers.

2. Wenn der NPS-Server ein Mitglied einer RADIUS-Remoteservergruppe ist, konfigurieren Sie die NPS-Proxy mit der neuen IP-Adresse des NPS-Servers neu.

3. Wenn Sie den NPS-Server zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Verbindung zwischen dem Computer mit SQL Server und dem NPS-Server weiterhin ordnungsgemäß ausgeführt wird.

4. Wenn Sie IPsec zum Sichern von RADIUS-Datenverkehr zwischen dem NPS-Server und einen NPS-Proxy, Servern oder anderen Geräten bereitgestellt haben, neu konfigurieren Sie, die IPsec-Richtlinie oder der Verbindungssicherheitsregel in Windows-Firewall mit erweiterter Sicherheit die neue IP-Adresse des NPS-Servers verwenden.

5. Wenn der NPS-Server mehrfach vernetzt und den Server zum Binden an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie NPS-Port-Einstellungen mit der neuen IP-Adresse neu.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>So überprüfen die Konfiguration nach einem NPS-Proxy-IP-Adresse ändern

1. Konfigurieren Sie alle RADIUS-Clients, z.B. drahtlose Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS-Proxy.

2. Wenn der NPS-Proxy mehrfach vernetzt ist und den Proxy zum Binden an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie NPS-Port-Einstellungen mit der neuen IP-Adresse neu.

3. Konfigurieren Sie alle Mitglieder der alle RADIUS-Remoteservergruppen mit IP-Adresse des Proxyservers. Für diese Aufgabe, jeden NPS-Server, die der NPS-Proxy als RADIUS-Client konfiguriert ist:

    ein. Doppelklicken Sie auf **NPS (lokal)**, doppelklicken Sie auf **RADIUS-Clients und Servern**, klicken Sie auf **RADIUS-Clients**, und doppelklicken Sie dann im Detailbereich auf RADIUS-Clients, die Sie ändern möchten.

    b. RADIUS-Client **Eigenschaften**im **Adresse \(IP or DNS\)**, geben Sie die neue IP-Adresse des NPS-Proxy.

4. Wenn Sie die NPS-Proxy zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Verbindung zwischen dem Computer mit SQL Server und dem NPS-Proxy weiterhin ordnungsgemäß ausgeführt wird.

## <a name="verify-configuration-after-renaming-an-nps-server"></a>Überprüfen der Konfiguration nach der Umbenennung eines NPS-Servers

Wenn sich möglicherweise Situationen müssen Sie zum Ändern des Namens eines NPS-Server oder Proxy, z.B. Wenn Sie die Benennungskonventionen für Ihre Server neu entwerfen.

Wenn Sie einen NPS-Server oder Proxynamen ändern, ist es erforderlich, um Teile der NPS-Bereitstellung neu konfigurieren. 

Verwenden Sie die folgenden allgemeinen Richtlinien, um zu überprüfen, dass es sich bei eine Änderung Netzwerkzugriffsauthentifizierung, Autorisierung oder Kontoführung nicht unterbrochen wird.

Sie müssen ein Mitglied sein **Administratoren**, oder eine gleichwertige, um dieses Verfahren auszuführen.

### <a name="to-verify-configuration-after-an-nps-server-or-proxy-name-change"></a>So überprüfen die Konfiguration nach einer NPS-Server oder Proxy Namen ändern

1. Wenn der NPS-Server ein Mitglied einer RADIUS-Remoteservergruppe ist aus, und die Gruppe mit Computernamen anstelle von IP-Adressen konfiguriert ist, konfigurieren Sie die RADIUS-Remoteservergruppe mit dem neuen Namen des NPS-Server neu.

2. Wenn zertifikatbasierte Authentifizierungsmethoden auf dem NPS-Server bereitgestellt werden, wird die Änderung des Namens des Serverzertifikats ungültig. Sie können ein neues Zertifikat anfordern, vom Administrator Zertifizierungsstelle (CA) oder wenn der Computer auf einem Domänenmitgliedscomputer und Zertifikate automatisch registrieren, um Mitglieder der Domäne ist, können Sie Gruppenrichtlinien, um ein neues Zertifikat durch die automatische Registrierung aktualisieren. So aktualisieren Sie die Gruppenrichtlinie:

    ein. Öffnen Sie die Befehlszeile oder WindowsPowerShell.

    b. Typ **Gpupdate**, und drücken Sie dann die EINGABETASTE.


3. Nachdem Sie ein neues Serverzertifikat haben, bitten Sie Administrator der Zertifizierungsstelle das alte Zertifikat widerrufen. 

     Nachdem das alte Zertifikat gesperrt wird, weiterhin NPS verwenden, bis das alte Zertifikat abläuft. Standardmäßig bleibt das alte Zertifikat für einen maximalen Zeitraum von einer Woche und 10 Stunden gültig. Dieses Zeitraums ist möglicherweise unterschiedlich, je nachdem, ob nach Ablauf (Certificate Revocation List, CRL) und Transport Layer Security (TLS) Cache Zeit nach Ablauf von der Standardeinstellung geändert wurde. Ablaufdatum der Standard-Zertifikatsperrliste ist eine Woche. die standardmäßige TLS cache Ablauf 10 Stunden ist. 

     Wenn Sie NPS sofort Verwendung des neuen Zertifikats konfigurieren möchten, können jedoch Sie manuell Netzwerkrichtlinien mit dem neuen Zertifikat neu konfigurieren.

4. Nachdem das alte Zertifikat abgelaufen ist, beginnt NPS automatisch mit dem neuen Zertifikat. 

5. Wenn Sie den NPS-Server zur Verwendung von SQL Server-Protokollierung konfiguriert haben, stellen Sie sicher, dass die Verbindung zwischen dem Computer mit SQL Server und dem NPS-Server weiterhin ordnungsgemäß ausgeführt wird.

