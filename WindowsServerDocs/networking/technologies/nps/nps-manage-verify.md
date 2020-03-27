---
title: Überprüfen der Konfiguration nach NPS-Änderungen
description: Sie können dieses Thema verwenden, um die Konfiguration des Netzwerk Richtlinien Servers von Windows Server 2016 nach einer IP-Adresse oder einer Namensänderung auf dem Server zu überprüfen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5a99cfb62d3ce331ef2d90fe13afe99a6d14960c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315887"
---
# <a name="verify-configuration-after-nps-changes"></a>Überprüfen der Konfiguration nach NPS-Änderungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um die NPS-Konfiguration nach einer IP-Adresse oder einer Namensänderung auf dem Server zu überprüfen.

## <a name="verify-configuration-after-an-nps-ip-address-change"></a>Überprüfen der Konfiguration nach einer NPS-IP-Adressänderung

Es kann Situationen geben, in denen Sie die IP-Adresse eines NPS oder Proxys ändern müssen, z. b. Wenn Sie den Server in ein anderes IP-Subnetz verschieben. 

Wenn Sie eine NPS-oder Proxy-IP-Adresse ändern, müssen Teile der NPS-Bereitstellung neu konfiguriert werden. 

Verwenden Sie die folgenden allgemeinen Richtlinien, um zu überprüfen, ob eine IP-Adressänderung die Authentifizierung, Autorisierung oder die Kontoführung für Netzwerk Zugriffe in Ihrem Netzwerk für NPS-RADIUS-Server und RADIUS-Proxy Server nicht unterbricht.

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um diese Prozeduren ausführen zu können.

### <a name="to-verify-configuration-after-an-nps-ip-address-change"></a>So überprüfen Sie die Konfiguration nach einer NPS-IP-Adressänderung

1. Konfigurieren Sie alle RADIUS-Clients, z. b. drahtlos Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS neu.

2. Wenn das NPS Mitglied einer RADIUS-Remote Server Gruppe ist, konfigurieren Sie den NPS-Proxy mit der neuen IP-Adresse des NPS neu.

3. Wenn Sie den NPS für die Verwendung SQL Server Protokollierung konfiguriert haben, überprüfen Sie, ob die Konnektivität zwischen dem Computer, auf dem SQL Server und dem NPS ausgeführt wird, weiterhin ordnungsgemäß funktioniert

4. Wenn Sie IPSec zum Sichern des RADIUS-Datenverkehrs zwischen Ihrem NPS und einem NPS-Proxy oder anderen Servern oder Geräten bereitgestellt haben, konfigurieren Sie die IPSec-Richtlinie oder die Verbindungs Sicherheitsregel in der Windows-Firewall mit erweiterter Sicherheit neu, um die neue IP-Adresse des NPS zu verwenden.

5. Wenn der NPS mehrfach vernetzt ist und Sie den Server für die Bindung an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie die NPS-Port Einstellungen mit der neuen IP-Adresse neu.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>So überprüfen Sie die Konfiguration nach einer Änderung der IP-Adresse für NPS

1. Konfigurieren Sie alle RADIUS-Clients, z. b. drahtlos Zugriffspunkte und VPN-Server, mit der neuen IP-Adresse des NPS-Proxys neu.

2. Wenn der NPS-Proxy mehrfach vernetzt ist und Sie den Proxy für die Bindung an einen bestimmten Netzwerkadapter konfiguriert haben, konfigurieren Sie die NPS-Port Einstellungen mit der neuen IP-Adresse neu.

3. Konfigurieren Sie alle Mitglieder aller RADIUS-Remote Server Gruppen mit der Proxy Server-IP-Adresse neu. Um diese Aufgabe durchzuführen, bei jedem NPS, bei dem der NPS-Proxy als RADIUS-Client konfiguriert ist, gilt Folgendes:

    a. Doppelklicken Sie auf **NPS (lokal)** , doppelklicken Sie auf **RADIUS-Clients und-Server**, klicken Sie auf **RADIUS-Clients**, und doppelklicken Sie dann im Detailbereich auf den RADIUS-Client, den Sie ändern möchten.

    b. Geben Sie in RADIUS-Client **Eigenschaften**in **Address \(IP oder DNS\)** die neue IP-Adresse des NPS-Proxys ein.

4. Wenn Sie den NPS-Proxy so konfiguriert haben, dass SQL Server Protokollierung verwendet wird, überprüfen Sie, ob die Konnektivität zwischen dem Computer, auf dem SQL Server und dem NPS-Proxy ausgeführt wird,

## <a name="verify-configuration-after-renaming-an-nps"></a>Überprüfen der Konfiguration nach dem Umbenennen eines NPS

Möglicherweise gibt es Situationen, in denen Sie den Namen eines NPS oder Proxys ändern müssen, z. b. Wenn Sie die Benennungs Konventionen für Ihre Server umgestalten.

Wenn Sie einen NPS-oder Proxy Namen ändern, müssen Sie Teile der NPS-Bereitstellung neu konfigurieren. 

Verwenden Sie die folgenden allgemeinen Richtlinien, um zu überprüfen, ob eine Server Namensänderung die Authentifizierung, Autorisierung oder Kontoführung für den Netzwerk Zugriff nicht unterbricht.

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

### <a name="to-verify-configuration-after-an-nps-or-proxy-name-change"></a>So überprüfen Sie die Konfiguration nach einer NPS-oder Proxy Namensänderung

1. Wenn das NPS Mitglied einer RADIUS-Remote Server Gruppe ist und die Gruppe mit Computernamen anstelle von IP-Adressen konfiguriert ist, konfigurieren Sie die Remote-RADIUS-Server Gruppe mit dem neuen NPS-Namen neu.

2. Wenn auf dem NPS Zertifikat basierte Authentifizierungsmethoden bereitgestellt werden, wird das Serverzertifikat durch die Namensänderung ungültig. Sie können ein neues Zertifikat von der Zertifizierungsstelle (Certification Authority, ca) anfordern. wenn es sich bei dem Computer um einen Domänen Mitglieds Computer handelt und Sie Zertifikate für Domänen Mitglieder automatisch registrieren, können Sie Gruppenrichtlinie aktualisieren, um ein neues Zertifikat über die automatische Registrierung abzurufen. . So aktualisieren Sie Gruppenrichtlinie:

    a. Öffnen Sie die Eingabeaufforderung oder Windows PowerShell.

    b. Geben Sie **gpupdate** ein, und drücken Sie dann die EINGABETASTE.


3. Wenn Sie über ein neues Serverzertifikat verfügen, fordern Sie an, dass der Zertifizierungsstellen Administrator das alte Zertifikat widerrufen muss. 

     Nachdem das alte Zertifikat widerrufen wurde, wird es von NPS weiterhin verwendet, bis das alte Zertifikat abläuft. Standardmäßig bleibt das alte Zertifikat für eine maximale Zeit von einer Woche bis zu 10 Stunden gültig. Dieser Zeitraum kann je nachdem, ob der Ablauf der Zertifikat Sperr Liste (CRL) und der Timeout für den Transport Layer Security (TLS)-Cache geändert wurde, von den Standardeinstellungen abweichen. Der Standard Ablauf der CRL beträgt eine Woche. der Standardwert für die TLS-Cache Zeit beträgt 10 Stunden. 

     Wenn Sie NPS jedoch sofort für die Verwendung des neuen Zertifikats konfigurieren möchten, können Sie Netzwerk Richtlinien mit dem neuen Zertifikat manuell neu konfigurieren.

4. Nachdem das alte Zertifikat abgelaufen ist, beginnt NPS automatisch mit der Verwendung des neuen Zertifikats. 

5. Wenn Sie den NPS für die Verwendung SQL Server Protokollierung konfiguriert haben, überprüfen Sie, ob die Konnektivität zwischen dem Computer, auf dem SQL Server und dem NPS ausgeführt wird, weiterhin ordnungsgemäß funktioniert

