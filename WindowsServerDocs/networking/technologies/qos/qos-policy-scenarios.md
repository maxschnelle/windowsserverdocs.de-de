---
title: Szenarien für QoS-Richtlinien
description: Dieses Thema enthält Quality of Service (QoS)-Richtlinien Szenarien, in denen veranschaulicht wird, wie Gruppenrichtlinie verwendet wird, um den Netzwerk Datenverkehr spezifischer Anwendungen und Dienste in Windows Server 2016 zu priorisieren.
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d777824d8e88cdb4e96f669fba9a96269783443b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997256"
---
# <a name="qos-policy-scenarios"></a>Szenarien für QoS-Richtlinien

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie Informationen zu hypothetischen Szenarien, in denen veranschaulicht wird, wann und warum die QoS-Richtlinie verwendet werden soll.

Die beiden Szenarien in diesem Thema lauten wie folgt:

1. Priorisieren von Netzwerk Datenverkehr für eine Branchen Anwendung
2. Priorisieren von Netzwerk Datenverkehr für eine HTTP-Server Anwendung

>[!NOTE]
>Einige Abschnitte dieses Themas enthalten allgemeine Schritte, die Sie ausführen können, um die beschriebenen Aktionen auszuführen. Ausführlichere Anweisungen zum Verwalten der QoS-Richtlinie finden Sie unter [Verwalten der QoS](qos-policy-manage.md)-Richtlinie.

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>Szenario 1: Priorisieren des Netzwerkverkehrs für eine Branchen Anwendung

In diesem Szenario hat eine IT-Abteilung mehrere Ziele, die Sie durch die Verwendung der QoS-Richtlinie erreichen können:

- Sorgen Sie für eine bessere Netzwerkleistung für Unternehmens \- kritische Anwendungen.
- Sorgen Sie für eine bessere Netzwerkleistung für einen Schlüsselsatz von Benutzern, während Sie eine bestimmte Anwendung verwenden.
- Stellen Sie sicher, dass die Unternehmens \- weite Daten Sicherungs Anwendung die Netzwerkleistung nicht beeinträchtigt, indem zu viel Bandbreite gleichzeitig verwendet wird.

Die IT-Abteilung beschließt, die QoS-Richtlinie so zu konfigurieren, dass bestimmte Anwendungen priorisiert werden, indem DSCP-Werte für den Differenzierungs Dienst-Codepunkt verwendet \( \) werden, um den Netzwerk Datenverkehr zu klassifizieren und um Ihre Router so zu konfigurieren

>[!NOTE]
>Weitere Informationen zu DSCP finden Sie im Abschnitt **Definieren der QoS-Priorität über einen differenzierte Dienste Codepunkt** im Thema [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).

Zusätzlich zu den DSCP-Werten können von QoS-Richtlinien eine Drosselungs Rate angegeben werden. Die Drosselung hat den Einfluss, dass der gesamte ausgehende Datenverkehr, der der QoS-Richtlinie entspricht, auf eine bestimmte Senderate beschränkt wird.

### <a name="qos-policy-configuration"></a>QoS-Richtlinien Konfiguration

Mit drei separaten Zielen beschließt der IT-Administrator, drei verschiedene QoS-Richtlinien zu erstellen.

#### <a name="qos-policy-for-lob-app-servers"></a>QoS-Richtlinie für Lob-App-Server

Die erste Unternehmens \- wichtige Anwendung, für die die IT-Abteilung eine QoS-Richtlinie erstellt, ist eine Unternehmens \- weite Ressourcenplanungs- \( ERP- \) Anwendung. Die ERP-Anwendung wird auf mehreren Computern gehostet, auf denen alle Windows Server 2016 ausgeführt werden. In Active Directory Domain Services sind diese Computer Mitglieder einer Organisationseinheit der Organisations \( Einheit \) , die für branchenspezifische \( LOB- \) Anwendungsserver erstellt wurde. Die Client \- seitige Komponente für die ERP-Anwendung wird auf Computern installiert, auf denen Windows 10 und Windows 8.1 ausgeführt werden.

In Gruppenrichtlinie wählt ein IT-Administrator das Gruppenrichtlinie Objekt- \( GPO aus, \) auf das die QoS-Richtlinie angewendet wird. Mit dem QoS-Richtlinien-Assistenten erstellt der IT-Administrator eine QoS-Richtlinie mit dem Namen "Server LOB Policy", die einen \- DSCP-Wert mit hoher Priorität 44 für alle Anwendungen, alle IP-Adressen, TCP und UDP sowie die Portnummer angibt.

Die QoS-Richtlinie wird nur auf die Lob-Server angewendet, indem das GPO mit der Organisationseinheit verknüpft wird, die nur diese Server enthält, über das Gruppenrichtlinien-Verwaltungskonsole \( GPMC- \) Tool. Diese erste Server-LOB-Richtlinie wendet den DSCP-Wert mit hoher Priorität an, \- Wenn der Computernetzwerk Datenverkehr sendet. Diese QoS-Richtlinie kann später \( im Gruppenrichtlinienobjekt-Editor Tool bearbeitet werden \) , um die Portnummern der ERP-Anwendung einzuschließen. Dadurch wird die Richtlinie so eingeschränkt, dass Sie nur angewendet wird, wenn die angegebene Portnummer verwendet wird.

#### <a name="qos-policy-for-the-finance-group"></a>QoS-Richtlinie für die Gruppe "Finanzen"

Während viele Gruppen innerhalb des Unternehmens auf die ERP-Anwendung zugreifen, hängt die Gruppe Finance von der Anwendung ab, wenn Sie mit den Kunden zusammenarbeiten, und die Gruppe erfordert eine konsistente hohe Leistung der app.

Um sicherzustellen, dass die Finanzgruppe Ihre Kunden unterstützen kann, muss die QoS-Richtlinie den Datenverkehr dieser Benutzer als hohe Priorität klassifizieren. Die Richtlinie sollte jedoch nicht angewendet werden, wenn Mitglieder der Finance-Gruppe andere Anwendungen als die ERP-Anwendung verwenden.

Daher definiert die IT-Abteilung im Gruppenrichtlinienobjekt-Editor Tool eine zweite QoS-Richtlinie mit dem Namen "Client-Lob-Richtlinie", die den DSCP-Wert 60 anwendet, wenn die Benutzergruppe "Finance" die ERP-Anwendung ausführt.

#### <a name="qos-policy-for-a-backup-app"></a>QoS-Richtlinie für eine Sicherungs-App

Auf allen Computern wird eine separate Sicherungs Anwendung ausgeführt. Um sicherzustellen, dass der Datenverkehr der Sicherungs Anwendung nicht alle verfügbaren Netzwerkressourcen verwendet, erstellt die IT-Abteilung eine Sicherungsdaten Richtlinie. Diese Sicherungs Richtlinie gibt den DSCP-Wert 1 Basierend auf dem ausführbaren Namen der Backup-APP an, der **backup.exe**wird.

Ein drittes GPO wird erstellt und für alle Client Computer in der Domäne bereitgestellt. Wenn die Sicherungs Anwendung Daten sendet, wird der DSCP-Wert mit niedriger Priorität angewendet, auch wenn er von Computern in der Finanzabteilung stammt.

>[!NOTE]
>Netzwerk Datenverkehr ohne QoS-Richtlinie wird mit einem DSCP-Wert von 0 gesendet.

### <a name="scenario-policies"></a>Szenariorichtlinien

In der folgenden Tabelle werden die QoS-Richtlinien für dieses Szenario zusammengefasst.

|Richtlinienname|DSCP-Wert|Drosselungs Rate|Auf Organisationseinheiten angewendet|BESCHREIBUNG|
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[Keine Richtlinie]|0|Keine|[Keine Bereitstellung]|Best mögliche Behandlung von nicht klassifiziertem Datenverkehr (Standard).|
|Sicherungsdaten|1|Keine|Alle Clients|Wendet einen DSCP-Wert mit niedriger Priorität für diese Massendaten an.|
|Server-LOB|44|Keine|Computer-OU für ERP-Server|Wendet DSCP mit hoher Priorität für den ERP-Server Datenverkehr an|
|Client-Lob|60|Keine|Finanz Benutzergruppe|Wendet DSCP mit hoher Priorität für den ERP-Client Datenverkehr an|

>[!NOTE]
>DSCP-Werte werden in Dezimalform dargestellt.

Wenn die QoS-Richtlinien mithilfe von Gruppenrichtlinie definiert und angewendet werden, empfängt der ausgehende Netzwerk Datenverkehr den von der Richtlinie angegebenen DSCP-Wert. Router stellen dann mithilfe von Warteschlangen eine differenzielle Behandlung auf Grundlage dieser DSCP-Werte bereit. Für diese IT-Abteilung werden die Router mit vier Warteschlangen konfiguriert: mit hoher Priorität, mit mittlerer Priorität, mit dem besten Aufwand und mit niedriger Priorität.

Wenn der Datenverkehr auf dem Router mit DSCP-Werten von "Server-LOB-Richtlinie" und "Client-Lob-Richtlinie" eingeht, werden die Daten in Warteschlangen mit hoher Priorität eingefügt. Datenverkehr mit einem DSCP-Wert von 0 (null) empfängt eine Dienst Ebene mit dem besten Aufwand Pakete mit einem DSCP-Wert von 1 (aus der Sicherungs Anwendung) erhalten eine Behandlung mit niedriger Priorität.

### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>Voraussetzungen für die Priorisierung einer Branchen Anwendung

Um diese Aufgabe abzuschließen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

- Auf den beteiligten Computern werden QoS- \- kompatible Betriebssysteme ausgeführt.

- Die beteiligten Computer sind Mitglieder einer Active Directory Domain Services \( AD DS \) Domäne, damit Sie mit Gruppenrichtlinie konfiguriert werden können.

- TCP/IP-Netzwerke werden mit Routern eingerichtet, die für DSCP \( RFC 2474 konfiguriert sind \) . Weitere Informationen finden Sie unter [RFC 2474](https://www.ietf.org/rfc/rfc2474.txt).

- Die Anforderungen an administrative Anmelde Informationen sind erfüllt.

#### <a name="administrative-credentials"></a>Administratoranmeldeinformationen

Zum Ausführen dieser Aufgabe müssen Sie in der Lage sein, Gruppenrichtlinie Objekte zu erstellen und bereitzustellen.

#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>Einrichten der Testumgebung für die Priorisierung einer Branchen Anwendung

Um die Testumgebung einzurichten, führen Sie die folgenden Aufgaben aus.

- Erstellen Sie eine AD DS Domäne mit Clients und Benutzern, die in Organisationseinheiten gruppiert sind. Anweisungen zum Bereitstellen von AD DS finden Sie im Handbuch zum Haupt [Netzwerk](../../core-network-guide/core-network-guide.md).

- Konfigurieren Sie die Router, um die Warteschlange basierend auf den DSCP-Werten zu differenzieren. Der DSCP-Wert 44 wechselt z. b. in eine "Platin"-Warteschlange, und alle anderen werden gewichtet mit einem Wert in der Warteschlange

>[!NOTE]
> Sie können DSCP-Werte mithilfe von Netzwerk Erfassungen mit Tools wie Netzwerkmonitor anzeigen. Nachdem Sie eine Netzwerk Erfassung durchgeführt haben, können Sie das Feld "TOS" in erfassten Daten beobachten.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>Schritte zum priorisieren einer Branchen Anwendung

Führen Sie die folgenden Aufgaben aus, um eine Branchen Anwendung zu priorisieren:

1. Erstellen und verknüpfen Sie ein Gruppenrichtlinie-Objekt- \( GPO \) mit einer QoS-Richtlinie.

2. Konfigurieren Sie die Router so, dass eine Branchen Anwendung (mithilfe von Warteschlangen) basierend auf den ausgewählten DSCP-Werten differenziert behandelt werden. Die Prozeduren dieser Aufgabe variieren in Abhängigkeit von der Art der routerart.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>Szenario 2: Priorisieren des Netzwerk Datenverkehrs für eine HTTP-Server Anwendung

In Windows Server 2016 enthält die Richtlinien basierte QoS die URL-basierten Features. Mit URL-Richtlinien können Sie die Bandbreite für http-Server verwalten.

Viele Unternehmensanwendungen werden für Internetinformationsdienste IIS-Webserver entwickelt und gehostet \( \) , und der Zugriff auf die Web-Apps erfolgt über Browser auf Client Computern.

In diesem Szenario wird davon ausgegangen, dass Sie eine Gruppe von IIS-Servern verwalten, die Schulungsvideos für alle Mitarbeiter Ihrer Organisation hosten. Ihr Ziel: Sie müssen sicherstellen, dass der Datenverkehr von diesen Videoservern Ihr Netzwerk nicht überlastet, und sicherstellen, dass Video Datenverkehr von Sprach-und Datenverkehr im Netzwerk unterschieden wird.

Die Aufgabe ähnelt der Aufgabe in Szenario 1. Sie entwerfen und konfigurieren die Einstellungen für die Datenverkehrs Verwaltung, z. b. den DSCP-Wert für den Video Datenverkehr, und die Drosselungs Rate wie bei Branchen Anwendungen. Wenn Sie jedoch den Datenverkehr angeben, geben Sie nicht den Anwendungsnamen an, sondern nur die URL, auf die die http-Serveranwendung antwortet: z https://hrweb/training . b..

> [!NOTE]
>URL-basierte QoS-Richtlinien können nicht verwendet werden, um den Netzwerk Datenverkehr für Computer mit Windows-Betriebssystemen zu priorisieren, die vor Windows 7 und Windows Server 2008 R2 veröffentlicht wurden.

### <a name="precedence-rules-for-url-based-policies"></a>Rang Folge Regeln für URL-basierte Richtlinien

Alle folgenden URLs sind gültig und können in der QoS-Richtlinie angegeben und gleichzeitig auf einen Computer oder einen Benutzer angewendet werden:

- https://video

- https://training.hr.mycompany.com

- https://10.1.10.249:8080/tech

- https://*/eBooks

Aber welche erhält Vorrang? Die Regeln sind einfach. URL-basierte Richtlinien werden in einer Lesefolge von links nach rechts priorisiert. Von der höchsten Priorität bis zur niedrigsten Priorität lauten die URL-Felder wie folgt:

[1. URL-Schema](#bkmk_QoS_UrlScheme)

[2. URL-Host](#bkmk_QoS_UrlHost)

[3. URL-Port](#bkmk_QoS_UrlPort)

[4. URL-Pfad](#bkmk_QoS_UrlPath)

Die Details lauten wie folgt:

####  <a name="1-url-scheme"></a><a name="bkmk_QoS_UrlScheme"></a>1. URL-Schema

 `https://`hat eine höhere Priorität als `https://` .

####  <a name="2-url-host"></a><a name="bkmk_QoS_UrlHost"></a>2. URL-Host

 Von der höchsten Priorität bis zur niedrigsten:

1. Hostname

2. IPv6-Adresse

3. IPv4-Adresse

4. Platzhalter

Im Fall von Hostname hat ein Hostname mit mehr gepunkteten Elementen (mehr Tiefe) eine höhere Priorität als ein Hostname mit weniger gepunkteten Elementen. Beispielsweise unter den folgenden Hostnamen:

- Video.Internal.Training.hr.mycompany.com (Tiefe = 6)

- selfguide.Training.mycompany.com (Tiefe = 4)

- Training (Tiefe = 1)

- Bibliothek (Tiefe = 1)

  **Video.Internal.Training.hr.mycompany.com** hat die höchste Priorität, und **selfguide.Training.mycompany.com** hat die nächsthöhere Priorität. **Training** und **Bibliothek** haben dieselbe niedrigste Priorität.

####  <a name="3-url-port"></a><a name="bkmk_QoS_UrlPort"></a>3. URL-Port

Eine bestimmte oder eine implizite Portnummer hat eine höhere Priorität als ein Platzhalter Port.

####  <a name="4-url-path"></a><a name="bkmk_QoS_UrlPath"></a>4. URL-Pfad

Ein URL-Pfad kann wie ein Hostname aus mehreren Elementen bestehen. Das Element mit mehr Elementen hat immer eine höhere Priorität als die mit less. Die folgenden Pfade sind z. b. nach Priorität aufgeführt:

1.  /ebooks/tech/windows/networking/qos

2.  /ebooks/tech/windows/

3.  /ebooks

4.  /

Wenn ein Benutzer sich entscheidet, alle Unterverzeichnisse und Dateien nach einem URL-Pfad einzubeziehen, hat dieser URL-Pfad eine niedrigere Priorität als wenn die Auswahl nicht getroffen wurde.

Ein Benutzer kann auch eine Ziel-IP-Adresse in einer URL-basierten Richtlinie angeben. Die Ziel-IP-Adresse hat eine niedrigere Priorität als die zuvor beschriebenen vier URL-Felder.

### <a name="quintuple-policy"></a>Quintuple-Richtlinie

Eine quintuple-Richtlinie wird durch die Protokoll-ID, Quell-IP-Adresse, Quellport, Ziel-IP-Adresse und Zielport angegeben. Eine quintuple-Richtlinie hat immer Vorrang vor jeder URL-basierten Richtlinie.

Wenn eine quintuple-Richtlinie bereits für einen Benutzer angewendet wird, verursacht eine neue URL-basierte Richtlinie keine Konflikte auf den Client Computern dieses Benutzers.

Das nächste Thema in dieser Anleitung finden Sie unter [Verwalten der QoS-Richtlinie](qos-policy-manage.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).