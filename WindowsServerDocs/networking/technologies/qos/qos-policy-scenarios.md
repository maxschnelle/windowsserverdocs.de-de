---
title: QoS-Richtlinie-Szenarien
description: Dieses Thema enthält die Richtlinie für Quality of Service (QoS)-Szenarien, die Verwendung von Gruppenrichtlinien zu verwenden, um den Netzwerkdatenverkehr über bestimmte Anwendungen und Dienste in Windows Server 2016 zu priorisieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2617c897ed2ea173d29fc7c4a87e52557154d463
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446990"
---
# <a name="qos-policy-scenarios"></a>QoS-Richtlinie-Szenarien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Können Sie in diesem Thema um hypothetische Szenarien zu überprüfen, die veranschaulichen, wie, wann und warum die QoS-Richtlinie verwenden.

Die beiden Szenarien in diesem Thema sind:

1. Priorisieren von Netzwerkdatenverkehr für eine Line-of-Business-Anwendung
2. Priorisieren von Netzwerkdatenverkehr für eine HTTP-Server-Anwendung

>[!NOTE]
>Einige Abschnitte dieses Themas enthalten die allgemeinen Schritte, die Sie zum Ausführen der beschriebenen Vorgänge ausführen können. Ausführlichere Anweisungen zum Verwalten von QoS-Richtlinie finden Sie unter [QoS-Richtlinie verwalten](qos-policy-manage.md).

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>Szenario 1: Priorisieren von Netzwerkdatenverkehr für eine Line-of-Business-Anwendung

In diesem Szenario hat die IT-Abteilung mehrere Ziele, die sie mithilfe von QoS-Richtlinie ausführen können:

- Geben Sie eine bessere Leistung des Netzwerks für unternehmenskritische\-kritische Anwendungen.
- Geben Sie eine bessere Leistung des Netzwerks für eine wichtige Gruppe von Benutzern, während sie eine bestimmte Anwendung verwenden werden.
- Stellen Sie sicher, dass das Unternehmen\-große Data Backup-Anwendung nicht beeinträchtigt Netzwerk mithilfe von zu viel Bandbreite auf einmal.

Die IT-Abteilung entscheidet sich so konfigurieren Sie QoS-Richtlinie, um bestimmte Anwendungen zu priorisieren, indem Sie mit Code-Dienstpunkt Differenzierung \(DSCP\) Werte zum Klassifizieren von Netzwerkdatenverkehr und die Router Zugriffscode zu konfigurieren die Behandlung für Datenverkehr mit höherer Priorität. 

>[!NOTE]
>Weitere Informationen zu DSCP, finden Sie im Abschnitt **definieren QoS-Priorität über ein Differentiated Services Code-Punkt** im Thema [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

Zusätzlich zu den DSCP-Werten können die QoS-Richtlinien eine Drosselungsrate angeben. Drosselung wirkt sich das Begrenzen des gesamten ausgehenden Datenverkehr, entspricht die QoS-Richtlinie für eine bestimmte Rate senden aus.

### <a name="qos-policy-configuration"></a>Konfiguration der QoS-Richtlinie

Der IT-Administrator möchte mit drei separaten Zielen zu erreichen erstellen Sie drei verschiedene QoS-Richtlinien.

#### <a name="qos-policy-for-lob-app-servers"></a>QoS-Richtlinie für LOB-App-Server

Das erste Ziel\-wichtige Anwendung, die für das Erstellen einer QoS-Richtlinie ist ein Unternehmen\-wide unternehmensressourcenplanung \(ERP\) Anwendung. Die ERP-Anwendung wird auf mehreren Computern gehostet, die alle Windows Server 2016 ausgeführt werden. In Active Directory Domain Services, werden diese Computer Mitglied einer Organisationseinheit \(Organisationseinheit\) erstellten LOB- \(LOB\) Anwendungsserver. Der Client\-serverseitige Komponenten für die ERP-Anwendung auf Computern mit Windows 10 und Windows 8.1 installiert ist.

In der Gruppenrichtlinie, wählt die IT-Administrator das Gruppenrichtlinienobjekt \(GPO\) auf den die QoS-Richtlinie angewendet wird. Mithilfe des Assistenten für QoS-Richtlinie erstellt der IT-Administrator eine QoS-Richtlinie mit dem Namen "Server LOB Richtlinie", die angibt, dass einer hohes\-Priorität DSCP-Wert 44 für alle Anwendungen, alle IP-Adressen, TCP und UDP und Portnummer.

Die QoS-Richtlinie gilt nur für die LOB-Server durch das Verknüpfen des Gruppenrichtlinienobjekts für die Organisationseinheit, die nur von diesen Servern, über die Gruppenrichtlinien-Verwaltungskonsole enthält \(GPMC\) Tool. Diese ersten Server LOB-Richtlinie gilt das Tageshoch\-Priorität DSCP-Wert, wenn der Computer, den Netzwerkdatenverkehr sendet. Diese QoS-Richtlinie kann später bearbeitet werden \(im Gruppenrichtlinienobjekt-Editor-Tool\) sollen Portnummern verwendet die ERP-Anwendung, die beschränkt, die Richtlinie, um gelten nur, wenn die angegebene Portnummer verwendet wird.

#### <a name="qos-policy-for-the-finance-group"></a>QoS-Richtlinie für der Finance-Gruppe

Während viele Gruppen innerhalb des Unternehmens die ERP-Anwendung zugreifen, die Finance-Gruppe für diese Anwendung abhängig ist, beim Umgang mit Kunden und die Gruppe erfordert die konsistent hohe Leistung in der app.

Um sicherzustellen, dass die Finance-Gruppe mit Kunden unterstützen kann, muss dieser Benutzer Datenverkehr die QoS-Richtlinie mit hoher Priorität klassifiziert werden. Die Richtlinie sollte jedoch nicht angewendet, wenn Mitglieder der Finance-Gruppe andere Anwendungen als das ERP-Anwendung verwenden. 

Aus diesem Grund definiert die IT-Abteilung eine zweite QoS-Richtlinie namens "Client LOB Richtlinie" im Gruppenrichtlinienobjekt-Editor-Tool, das einen DSCP-Wert von 60 gilt, wenn die Finance-Gruppe für Benutzer die ERP-Anwendung ausgeführt wird.

#### <a name="qos-policy-for-a-backup-app"></a>QoS-Richtlinie für eine Backup-App

Eine separate Anwendung für die Sicherung wird auf allen Computern ausgeführt. Um sicherzustellen, dass die sicherungsanwendung Datenverkehr nicht alle verfügbaren Netzwerk-Ressourcen verwendet, erstellt die IT-Abteilung eine Richtlinie für die Sicherung von Daten. Diese Sicherungsrichtlinie gibt an, einen DSCP-Wert von 1 basierend auf den Namen der ausführbaren Datei für die backup-app handelt es sich **backup.exe**. 

Eine dritte GPO erstellt und für alle Clientcomputer in der Domäne bereitgestellt wurde. Wenn die backup-Anwendung Daten sendet, wird der DSCP-Wert mit niedriger Priorität angewendet, selbst wenn er auf den Computern in der Finanzabteilung stammt.
  
>[!NOTE]
>Netzwerkdatenverkehr, ohne eine QoS-Richtlinie sendet, mit einem DSCP-Wert von 0.

### <a name="scenario-policies"></a>Szenariorichtlinien

In der folgende Tabelle werden die QoS-Richtlinien für dieses Szenario zusammengefasst.
  
|Richtlinienname|DSCP-Wert|Drosselungsrate|Auf Organisationseinheiten angewendet|Beschreibung|  
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[Keine Richtlinie]|0|Keine|[Keine-Bereitstellung]|Beste Aufwand (Standard)-Behandlung für nicht klassifizierte Datenverkehr.|  
|Sicherungsdaten|1|Keine|Alle clients|Wendet einen DSCP-Wert mit niedriger Priorität für diese Daten Bulk an.|  
|LOB-Server|44|Keine|Computer-OE für ERP-Server|Gilt wichtiges DSCP für ERP-Server-Datenverkehr|  
|LOB-Client|60|Keine|Gruppe der Finance-Benutzer|Gilt wichtiges DSCP für Clientdatenverkehr ERP|  

>[!NOTE]
>DSCP-Werte werden im Dezimalformat dargestellt.

Mit QoS-Richtlinien definiert und mithilfe der Gruppenrichtlinie angewendet empfängt die ausgehenden Netzwerkdatenverkehr den Richtlinie angegebenen DSCP-Wert. Anschließend erhalten Router differenzielle behandelt, die basierend auf diesen DSCP-Werten mithilfe von Warteschlangen. Für diese IT-Abteilung, die Router mit vier Warteschlangen konfiguriert sind: hoher Priorität, mittlerer Priorität, Best-Effort-Prinzip und mit niedriger Priorität.

Wenn Datenverkehr empfangen, auf dem Router mit DSCP-Werten aus "Server LOB Richtlinie" und "Client LOB-Richtlinie" befindet sich die Daten in Warteschlangen mit hoher Priorität. Datenverkehr mit einem DSCP-Wert von 0 erhält einen Best-Effort-Prinzip Servicelevel. Pakete mit einem DSCP-Wert von 1 (aus der sicherungsanwendung) erhalten mit niedriger Priorität behandelt.  
  
### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>Voraussetzungen für die Priorisierung einer Line-of-Business-Anwendung

Um diese Aufgabe abzuschließen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

- Die beteiligten Computern laufen QoS\-kompatiblen Betriebssystemen.

- Die betroffenen Computer sind Mitglieder einer Active Directory-Domänendienste \(AD DS\) Domäne, damit sie mithilfe der Gruppenrichtlinie konfiguriert werden können.

- TCP/IP-Netzwerken mit Routern, die für die DSCP konfiguriert eingerichtet sind \(RFC 2474\). Weitere Informationen finden Sie unter [RFC 2474](https://www.ietf.org/rfc/rfc2474.txt).

- Administratoranmeldeinformationen sind erfüllt.

#### <a name="administrative-credentials"></a>Administratoranmeldeinformationen

Um diese Aufgabe abzuschließen, müssen Sie sein können, erstellen und Bereitstellen von Gruppenrichtlinienobjekten.
  
#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>Einrichten der testumgebung für die Priorisierung einer Line-of-Business-Anwendung

Informationen zum Einrichten der testumgebung können führen Sie die folgenden Aufgaben aus.

- Erstellen einer AD DS-Domäne mit Clients und Benutzern in Organisationseinheiten gruppiert. Anweisungen zum Bereitstellen von AD DS finden Sie die [Core Network Guide](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide).

- Konfigurieren Sie den Router differentially Warteschlange basierend auf den DSCP-Werten. Klicken Sie z. B. DSCP-Wert 44 gibt eine Warteschlange "Platinum", und alle anderen sind gewichtet Fair-Warteschlange.

>[!NOTE]
> Sie können DSCP-Werten mithilfe von netzwerkerfassungen mit Tools wie Network Monitor anzeigen. Nachdem Sie eine netzwerkerfassung ausgeführt haben, können Sie das TOS-Feld im erfassten Daten beobachten.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>Schritte für die Priorisierung einer Line-of-Business-Anwendung

Um eine Line-of-Business-Anwendung zu priorisieren, können führen Sie die folgenden Aufgaben aus:

1. Erstellen und Verknüpfen eines Gruppenrichtlinienobjekts \(GPO\) mit einer QoS-Richtlinie.

2. Konfigurieren Sie die Router so, dass eine Line-of-Business differentially behandeln Anwendung (mithilfe von Warteschlangen) basierend auf den ausgewählten DSCP-Werten. Die Verfahren in dieser Aufgabe variiert je nach Art der Router, was man.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>Szenario 2: Priorisieren von Netzwerkdatenverkehr für eine HTTP-Server-Anwendung

In Windows Server 2016 enthält richtlinienbasierten QoS die URL-basierte Richtlinien-Funktion. URL-Richtlinien können Sie die Bandbreite für HTTP-Servern zu verwalten.

Viele unternehmensanwendungen für entwickelt und in Internet Information Services gehosteten \(IIS\) Webserver und die Web-apps von Browsern auf den Clientcomputern erfolgt.

In diesem Szenario wird davon ausgegangen Sie, dass Sie einem Satz von IIS-Server, Host-Schulungsvideos für Mitarbeiter Ihres Unternehmens verwalten. Ihr Ziel ist, um sicherzustellen, dass der Datenverkehr über diese Videos Server Ihr Netzwerk überlasten keine, und stellen Sie sicher, dass die video-Datenverkehr von Sprach- und Datenverkehr im Netzwerk unterschieden wird. 

Die Aufgabe ähnelt der Aufgabe in Szenario 1. Sie entwerfen und Konfigurieren von Einstellungen für die datenverkehrsverwaltung, z. B. den DSCP-Wert für die video-Datenverkehr und die Drosselung gleich bewerten, wie Sie für die LOB-Anwendungen. Jedoch beim Angeben des Datenverkehrs, statt den Anwendungsnamen, geben Sie nur die URL, die die HTTP-Server-Anwendung antwortet: z. B. https://hrweb/training.
  
> [!NOTE]
>URL-basierter QoS-Richtlinien können keine zur Priorisierung des Netzwerkverkehrs für Computer mit Windows-Betriebssystemen, die vor Windows 7 und Windows Server 2008 R2 veröffentlicht wurden.

### <a name="precedence-rules-for-url-based-policies"></a>Rangfolgeregeln für URL-basierte Richtlinien

Die folgenden URLs sind gültig und können in QoS-Richtlinie angegeben, und gleichzeitig auf einem Computer oder Benutzer angewendet:

- https://video

- https://training.hr.mycompany.com

- https://10.1.10.249:8080/tech  

- https://*/ebooks

Aber welche erhalten Vorrang vor? Die Regeln sind einfach. URL-basierte Richtlinien werden in einer links-nach-rechts-Lesefolge priorisiert. Sind also von der höchsten Priorität die niedrigste Priorität, die URL-Felder:
  
[1. URL-Schema](#bkmk_QoS_UrlScheme)

[2. URL-host](#bkmk_QoS_UrlHost)

[3. URL-port](#bkmk_QoS_UrlPort)

[4. URL-Pfad](#bkmk_QoS_UrlPath)

Details lauten wie folgt aus:

####  <a name="bkmk_QoS_UrlScheme"></a> 1. URL-Schema

 `https://` hat eine höhere Priorität als `https://`.

####  <a name="bkmk_QoS_UrlHost"></a> 2. URL-host

 Von der höchsten Priorität, mit der zweitniedrigsten sind sie folgende Aktionen ausführen:

1. Hostname

2. IPv6-Adresse

3. IPv4-Adresse

4. Platzhalter

Im Fall von Hostname hat ein Hostnamen mit mehr gepunktete Elementen (genauer) eine höhere Priorität als einen Hostnamen mit weniger gepunktete Elemente. Z. B. für die folgenden Hostnamen verwenden:

- video.internal.training.hr.mycompany.com (depth = 6)
  
- selfguide.training.mycompany.com (depth = 4)
  
- Training (Depth = 1)
  
- Bibliothek (Depth = 1)
  
  **Video.Internal.Training.hr.mycompany.com** hat die höchste Priorität, und **selfguide.training.mycompany.com** die nächstniedrigeren Priorität hat. **Training** und **Bibliothek** teilen die gleiche niedrigste Priorität.  
  
####  <a name="bkmk_QoS_UrlPort"></a> 3. URL-port

Verfügt über eine höhere Priorität als ein Platzhalter-Port, ein bestimmtes oder eine implizite Portnummer.

####  <a name="bkmk_QoS_UrlPath"></a> 4. URL-Pfad

Ein URL-Pfad kann z. B. einem Hostnamen mehrere Elemente enthalten. Das Element mit mehreren Elementen verfügt immer über eine höhere Priorität als die mit weniger Aufwand. Die folgenden Pfade sind z. B. nach Priorität aufgeführt:  

1.  /ebooks/tech/windows/networking/qos

2.  /ebooks/tech/windows/

3.  /ebooks

4.  /

Wenn ein Benutzer entscheidet, die alle Unterverzeichnisse und Dateien, die nach einem URL-Pfad enthalten, müssen diese URL-Pfad eine niedrigere Priorität, als hätte, wenn die Auswahl nicht vorgenommen wurden.

Ein Benutzer kann auch an eine Ziel-IP-Adresse in einer URL-basierte Richtlinie auswählen. Die Ziel-IP-Adresse hat eine niedrigere Priorität als die vier URL-Felder, die zuvor beschriebenen.
  
### <a name="quintuple-policy"></a>Quintupel Richtlinie

Eine Quintupel Richtlinie wird durch die Protokoll-ID, IP-Quelladresse, Quellport, IP-Zieladresse und Zielport angegeben. Eine Quintupel Richtlinie hat immer Vorrang vor einer URL-basierte Richtlinie. 

Wenn eine Quintupel Richtlinie bereits für einen Benutzer angewendet wird, wird eine neue URL-basierte Richtlinie nicht Konflikte auf Client-dieses Benutzers Computer verursacht.

Im nächsten Thema in diesem Handbuch finden Sie unter [QoS-Richtlinie verwalten](qos-policy-manage.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
