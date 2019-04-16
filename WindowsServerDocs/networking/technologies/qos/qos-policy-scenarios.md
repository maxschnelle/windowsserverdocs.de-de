---
title: QoS-Richtlinie-Szenarien
description: Dieses Thema enthält Richtlinien für Quality of Service (QoS)-Szenarien, die demonstriert, wie Sie Gruppenrichtlinien verwenden, um den Netzwerkdatenverkehr von bestimmten Anwendungen und Diensten in Windows Server2016 zu priorisieren.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b635f73cc25552f4c1a05f8db6303f636eda3c54
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-scenarios"></a>QoS-Richtlinie-Szenarien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema hypothetische Szenarien zu überprüfen, die veranschaulichen, wie, wann, und wie Sie QoS-Richtlinie verwenden.

Die beiden Szenarien in diesem Thema sind:

1. Priorisieren der Netzwerkverkehr für eine Line-of-Business-Anwendung
2. Priorisieren der Netzwerkverkehr für eine HTTP-Server-Anwendung

>[!NOTE]
>Einige Abschnitte dieses Themas enthalten die allgemeinen Schritte, mit denen Sie die beschriebenen Aktionen ausführen können. Ausführlichere Informationen zur Verwaltung von QoS-Richtlinie finden Sie unter [QoS-Richtlinie verwalten](qos-policy-manage.md).

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>Szenario 1: Priorisieren des Netzwerkdatenverkehrs für eine Line-of-Business-Anwendung

In diesem Szenario hat die IT-Abteilung mehrere Ziele, die sie ausführen können, mithilfe von QoS-Richtlinie:

- Bieten Sie eine bessere netzwerkleistung für Mission\ erforderliche Anwendungen.
- Bereitstellen Sie aus Leistungsgründen Netzwerk für einen Schlüsselsatz von Benutzern, während sie eine bestimmte Anwendung verwenden.
- Stellen Sie sicher, dass die Daten für die gesamte Company\ Backup Anwendung Leistung des Netzwerks beeinträchtigen nicht mithilfe von zu viel Bandbreite auf einmal.

Die IT-Abteilung entscheidet sich für das Konfigurieren von QoS-Richtlinie, um bestimmte Anwendungen zu priorisieren, mithilfe der Differenzierung Service Code Point \(DSCP\) Werte, den Netzwerkverkehr zu klassifizieren und so konfigurieren Sie den Router so, dass bevorzugte Behandlung für Datenverkehr mit höherer Priorität angeben. 

>[!NOTE]
>Weitere Informationen zu DSCP, finden Sie im Abschnitt **definieren QoS-Priorität über ein Differentiated Services Code Point** im Thema [Quality of Service (QoS)-Richtlinie ](qos-policy-top.md).

Neben der DSCP-Werte können QoS-Richtlinien für eine Drosselungsrate angeben. Einschränkung hat die Auswirkung der gesamte ausgehenden Datenverkehr, entspricht die QoS-Richtlinie für einen bestimmten Satz senden zu beschränken.

### <a name="qos-policy-configuration"></a>Konfiguration der QoS-Richtlinie

Mit drei separaten Ziele zu erreichen entscheidet sich IT-Administratoren drei verschiedene QoS-Richtlinien erstellen.

#### <a name="qos-policy-for-lob-app-servers"></a>QoS-Richtlinie für LOB-App-Server

Die erste Mission\ erforderliche Anwendung, die für die die IT-Abteilung eine QoS-Richtlinie erstellt ist eine Enterprise-Ressource für Company\-Wide, das Planen \(ERP\) Anwendung. Die ERP-Anwendung wird auf mehreren Computern gehostet, die alle Windows Server2016 ausgeführt werden. In Active Directory Domain Services, diese Computer sind Mitglieder einer Organisationseinheit \(OU\), die für Anwendungsserver, Line-of-Business-\(LOB\) erstellt wurde. Die Client-Side-Komponente für die ERP-Anwendung ist auf Computern installiert, auf denen Windows10 und Windows8.1 ausgeführt werden.

In der Gruppenrichtlinie wählt ein IT-Administrator den Gruppenrichtlinienobjekt-\(GPO\) auf dem die QoS-Richtlinie angewendet wird. Mithilfe des Assistenten für die QoS-Richtlinie erstellt der IT-Administrator eine QoS-Richtlinie namens "Server LOB Richtlinie", einen allgemeine Priorität DSCP-Wert 44 für alle Anwendungen, IP-Adresse, TCP und UDP und Portnummer angibt.

Die QoS-Richtlinie gilt nur für die LOB-Server durch Verknüpfen des Gruppenrichtlinienobjekts mit der Organisationseinheit, die nur von diesen Servern, über die Gruppenrichtlinien-Verwaltungskonsole \(GPMC\) Tool enthält. Dieser ersten Server LOB-Richtlinie wird die allgemeine Priorität DSCP-Wert verwendet, wenn der Computer, den Netzwerkdatenverkehr sendet. Diese QoS-Richtlinie später bearbeitet werden kann \ (in der Gruppenrichtlinien-Editors Tool\) Portnummern ERP-Anwendung, enthalten die beschränkt, die Richtlinie anwenden, wenn die angegebene Portnummer verwendet wird.

#### <a name="qos-policy-for-the-finance-group"></a>QoS-Richtlinie für die Finance-Gruppe

Während viele Gruppen innerhalb des Unternehmens ERP-Anwendung den Zugriff auf die Finance-Gruppe auf diese Anwendung abhängig ist, beim Umgang mit Kunden, und die Gruppe erfordert durchgängig hohen Leistung der App.

Um sicherzustellen, dass die Finance-Gruppe ihre Kunden unterstützen kann, muss die QoS-Richtlinie dieser Benutzer Datenverkehr mit hoher Priorität klassifizieren. Allerdings sollten die Richtlinie nicht anwenden, wenn Mitglieder der Finance-Gruppe nur die ERP-Anwendung. 

Aus diesem Grund definiert die IT-Abteilung eine zweite QoS-Richtlinie namens "Client LOB Richtlinie" in der Gruppenrichtlinien-Editor-Tool, das einen DSCP-Wert 60 gilt, wenn die Benutzer Finanzgruppe ERP-Anwendung ausgeführt wird.

#### <a name="qos-policy-for-a-backup-app"></a>QoS-Richtlinie für eine App-Sicherung

Eine separate Anwendung wird auf allen Computern ausgeführt. Um sicherzustellen, dass die sicherungsanwendung Datenverkehr nicht alle verfügbaren Netzwerkressourcen verwendet wird, erstellt die IT-Abteilung eine Richtlinie für die Sicherung von Daten. Diese Sicherungsrichtlinie gibt einen DSCP-Wert von 1 basierend auf den Namen der ausführbaren Datei für die Sicherung App, die ist **Backup.exe **. 

Eine dritte Gruppenrichtlinienobjekt wird erstellt und für alle Clientcomputer in der Domäne bereitgestellt. Wenn die sicherungsanwendung Daten sendet, wird mit niedriger Priorität DSCP-Wert angewendet, auch wenn es von Computern in der Finanzabteilung stammt.
  
>[!NOTE]
>Netzwerkdatenverkehr, ohne eine QoS-Richtlinie wird mit dem DSCP-Wert 0 gesendet.

### <a name="scenario-policies"></a>Szenariorichtlinien

In der folgende Tabelle werden die QoS-Richtlinien für dieses Szenario zusammengefasst.
  
|Name der Richtlinie|DSCP-Wert|Drosselungsrate|Organisationseinheiten angewendet|Beschreibung|  
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[Keine Richtlinie]|0|Keine|[Kein Bereitstellung]|Beste Aufwand (Standard) Behandlung für den ungeschützten Datenverkehr.|  
|Sicherung von Daten|1|Keine|Alle Clients|Wendet einen DSCP-Wert mit niedriger Priorität für diese Datenmengen.|  
|LOB-Server|44|Keine|Computer Organisationseinheit für ERP-Server|Wendet mit hoher Priorität DSCP-Markierung für ERP-Server-Datenverkehr|  
|LOB-Client|60|Keine|Finance-Benutzer-Gruppe|Wendet mit hoher Priorität DSCP-Markierung für ERP-Client-Datenverkehr|  

>[!NOTE]
>DSCP-Werte werden im Dezimalformat dargestellt.

Mit QoS-Richtlinien definiert und mithilfe der Gruppenrichtlinie angewendet empfängt ausgehendem Netzwerkdatenverkehr den Richtlinie angegebene DSCP-Wert. Router sind dann differenzielle Behandlung basierend auf diesen DSCP-Werten mithilfe von queuing. Für diese IT-Abteilung die Router mit vier Warteschlangen konfiguriert sind: mit hoher Priorität, mittlerer Priorität, bestmöglichen und niedriger Priorität.

Wenn Datenverkehr eingeht, auf dem Router mit DSCP-Werten aus "Server LOB Richtlinie" und "Client LOB-Richtlinie" werden die Daten in Warteschlangen mit hoher Priorität platziert. Datenverkehr mit DSCP-Wert von 0 erhält eine bestmöglichen Service. Pakete mit einem DSCP-Wert von 1 (aus der Sicherung Anwendung) werden mit niedriger Priorität-behandelt.  
  
### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>Voraussetzungen für die Priorisierung einer Line-of-Business-Anwendung

Um diese Aufgabe abzuschließen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

- Beteiligten Computer werden QoS\-kompatiblen Betriebssysteme ausgeführt werden.

- Beteiligten Computer sind Mitglieder einer Active Directory-Domänendienste-Domäne \(AD DS\), sodass sie mithilfe von Gruppenrichtlinien konfiguriert werden können.

- TCP/IP-Netzwerken werden Router für DSCP \(RFC 2474\) konfiguriert eingerichtet. Weitere Informationen finden Sie unter [RFC 2474](http://www.ietf.org/rfc/rfc2474.txt).

- Administratoranmeldeinformationen erfüllt sind.

#### <a name="administrative-credentials"></a>Administrative Anmeldeinformationen

Um diese Aufgabe abzuschließen, müssen Sie möglicherweise zum Erstellen und Bereitstellen von Gruppenrichtlinienobjekten.
  
#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>Einrichten der Testumgebung für die Priorisierung einer Line-of-Business-Anwendung

Informationen zum Einrichten der Testumgebung führen Sie die folgenden Aufgaben aus.

- Erstellen einer AD DS-Domäne mit Clients und Benutzern in Organisationseinheiten gruppiert. Eine Anleitung zum Bereitstellen von AD DS finden Sie die [Kernnetzwerkhandbuch ](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide).

- Konfigurieren Sie die Router differentially Warteschlange, die basierend auf DSCP-Werten. Z.B. DSCP-Wert 44 wechselt in eine Warteschlange "Platinum", und alle anderen sind gewichtete Fair-Warteschlange.

>[!NOTE]
> Sie können DSCP-Werte mithilfe von Netzwerkaktivitäten mit Tools wie Network Monitor anzeigen. Nachdem Sie eine Aufzeichnung des Netzwerkdatenverkehrs durchgeführt haben, können Sie die TOS-Felds in erfassten Daten beobachten.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>Schrittefür die Priorisierung einer Line-of-Business-Anwendung

Um eine Line-of-Business-Anwendung zu priorisieren, führen Sie die folgenden Aufgaben aus:

1. Erstellen Sie und verknüpfen Sie ein Gruppenrichtlinienobjekt \(GPO\) mit einer QoS-Richtlinie.

2. Konfigurieren Sie den Router so, dass eine Line-of-Business differentially behandeln Anwendung (mithilfe von queuing) basierend auf den ausgewählten DSCP-Werten. Die Verfahren dieses Vorgangs variieren je nach Art der Router haben Sie.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>Szenario 2: Priorisieren des Netzwerkdatenverkehrs für eine HTTP-Server-Anwendung

In Windows Server2016 enthält Richtlinienbasierte QoS das Feature URL-basierte Richtlinien. URL-Richtlinien können Sie zum Verwalten der Bandbreite für HTTP-Server.

Viele unternehmensanwendungen entwickelt und auf Internetinformationsdienste \(IIS\) Webservern gehostet werden, und die Web-Apps von Browsern auf Clientcomputern aus zugegriffen werden.

In diesem Szenario wird davon ausgegangen Sie, dass Sie einer Reihe von IIS-Servern die Host-Schulungsvideos für Mitarbeiter Ihres Unternehmens verwalten. Ziel ist, um sicherzustellen, dass der Datenverkehr von diesen Servern Video nicht Ihrem Netzwerk überlasten und sicherzustellen, dass die Video-Datenverkehr von Sprach- und Datenverkehr im Netzwerk ausgeführt wird. 

Die Aufgabe ist die Aufgabe im Szenario 1 vergleichbar. Sie entwerfen und Konfigurieren von Einstellungen für die datenverkehrsverwaltung, z.B. den DSCP-Wert für das Video-Datenverkehr und die Einschränkung gleich bewerten, wie dies bei der Line-of-Business-Anwendungen. Beim Angeben des Datenverkehrs, anstatt den Namen der Anwendung, Sie jedoch nur eingeben die URL auf die die HTTP-Server-Anwendung reagiert werden: z. B.https://hrweb/training.
  
> [!NOTE]
>URL-basierter QoS-Richtlinien können Sie die Priorität des Netzwerkdatenverkehrs für Computer mit Windows-Betriebssystemen, die vor Windows7 und Windows Server2008 R2 veröffentlicht wurden.

### <a name="precedence-rules-for-url-based-policies"></a>Regeln für die URL-basierte Richtlinien

Alle folgenden URLs gültig sind und können in QoS-Richtlinie angegeben und gleichzeitig auf einem Computer oder Benutzer angewendet:

- http://video

- https://training.hr.mycompany.com

- http://10.1.10.249:8080/tech  

- https://*/ebooks

Aber welche erhalten Vorrang vor? Die Regeln sind einfach. URL-basierte Richtlinien werden in der leserichtung von links nach rechts priorisiert. Daher sind von der höchsten Priorität die niedrigste Priorität, die URL-Felder:
  
[1. URL-Schema](#bkmk_QoS_UrlScheme)

[2. URL-Host](#bkmk_QoS_UrlHost)

[3. URL-Port](#bkmk_QoS_UrlPort)

[4. URL-Pfad](#bkmk_QoS_UrlPath)

Detail sind wie folgt:

####  <a name="bkmk_QoS_UrlScheme"></a>1. URL-Schema

 `https://` Hat eine höhere Priorität als `http://`.

####  <a name="bkmk_QoS_UrlHost"></a>2. URL-Host

 Von der höchsten Priorität die niedrigste sind:

1. Hostname

2. IPv6-Adresse

3. IPv4-Adresse

4. Platzhalter

Im Fall von Hostnamen hat ein Hostnamen mit mehr gepunktete Elemente (genauer) eine höhere Priorität als einen Hostnamen mit weniger gepunktete Elemente. Beispielsweise unter den folgenden Hostnamen:

- Video.internal.training.hr.mycompany.com (Tiefe = 6)
  
- selfguide.training.mycompany.com (Tiefe = 4)
  
- Schulung (Depth = 1)
  
- Bibliothek (Depth = 1)
  
 **Video.internal.training.hr.mycompany.com** hat die höchste Priorität, und **selfguide.training.mycompany.com** die höchste Priorität hat. **Schulung** und **Bibliothek** teilen die gleiche Priorität.  
  
####  <a name="bkmk_QoS_UrlPort"></a>3. URL-Port

Ein bestimmtes oder eine implizite Portnummer verfügt über eine höhere Priorität als eine Platzhalter-Port.

####  <a name="bkmk_QoS_UrlPath"></a>4. URL-Pfad

Wie ein Hostname kann der URL-Pfad aus mehreren Elementen bestehen. Mit mehreren Elementen hat immer eine höhere Priorität als die mit weniger Aufwand. Beispielsweise sind die folgenden Pfade nach Priorität aufgeführt:  

1.  /eBooks/Tech/Windows/Networking/QoS

2.  / E-Books Tech/Windows /

3.  /ebooks

4.  /

Wenn ein Benutzer alle Unterverzeichnisse und Dateien, die nach den URL-Pfad enthalten möchte, müssen diese URL-Pfad eine niedrigere Priorität als bei der die Auswahl nicht vorgenommen wurden.

Benutzer können auch eine Ziel-IP-Adresse in einer URL-basierter Richtlinie angeben. Die Ziel-IP-Adresse verfügt über eine niedrigere Priorität als die vier URL-Felder, die zuvor beschriebenen.
  
### <a name="quintuple-policy"></a>Quintupel Richtlinie

Eine Quintupel Richtlinie wird vom Quell-IP-Adresse, Protokoll-ID, Quellport, Ziel-IP-Adresse und Zielport angegeben. Eine Quintupel Richtlinie hat immer eine höhere Priorität als URL-basierter Richtlinie. 

Wenn für einen Benutzer bereits eine Quintupel Richtlinie angewendet wird, wird eine neue URL-basierter Richtlinie nicht Konflikte auf einem Client des Benutzers Computer verursacht.

Im nächsten Thema in diesem Handbuch, finden Sie unter [QoS-Richtlinie verwalten ](qos-policy-manage.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
