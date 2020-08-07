---
title: 'Schritt 2: Konfigurieren des DirectAccess-VPN-Servers'
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: fe221fc9-c7d9-4508-b8a1-000d2515283c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a9206ca86f9b64036b9a16d29e6c442268c3d4ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953726"
---
#  <a name="step-2-configure-the-directaccess-vpn-server"></a>Schritt 2: Konfigurieren des DirectAccess-VPN-Servers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird die Konfiguration der Client- und Servereinstellungen erläutert, die für eine einfache Remotezugriffsbereitstellung mit dem Assistenten zum Aktivieren von DirectAccess erforderlich sind.

In der folgenden Tabelle finden Sie eine Übersicht über die Schritte, die Sie in diesem Thema ausführen können.

|Aufgabe       |BESCHREIBUNG|
|-----------|-----------|
|Konfigurieren von DirectAccess-Clients|Konfigurieren Sie den Remotezugriffsserver mit den Sicherheitsgruppen, die die DirectAccess-Clients enthalten.|
|Konfigurieren der Netzwerktopologie|Konfigurieren Sie die Einstellungen des RAS-Servers.|
|Konfigurieren der Suchliste für DNS-Suffixe|Ändern Sie die Suchliste für DNS-Suffixe bei Bedarf.|
|Konfiguration der Gruppenrichtlinienobjekte|Ändern Sie bei Bedarf die Gruppenrichtlinienobjekte.|

## <a name="to-start-the-enable-directacces-wizard"></a>So starten Sie den Assistenten zum Aktivieren von DirectAccess

1. Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **Remote Zugriff**. Der Assistent zum Aktivieren von DirectAccess wird automatisch gestartet, es sei denn, Sie haben den **Bildschirm nicht mehr anzeigen**ausgewählt.

2. Wenn der Assistent nicht automatisch startet, klicken Sie mit der rechten Maustaste auf den Serverknoten in der Struktur Routing und Remotezugriff und anschließend auf **DirectAccess aktivieren**.

3. Klicken Sie auf **Weiter**.

## <a name="configure-directaccess-clients"></a>Konfigurieren von DirectAccess-Clients

Damit ein Clientcomputer zur Verwendung von DirectAccess bereitgestellt werden kann, muss er zur ausgewählten Sicherheitsgruppe gehören. Nachdem DirectAccess konfiguriert wurde, werden Clientcomputer in der Sicherheitsgruppe bereitgestellt, damit sie das DirectAccess-Gruppenrichtlinienobjekt empfangen.

1. Klicken Sie auf der Seite **Gruppen auswählen** auf **Hinzufügen**.

2. Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die DirectAccess-Clientcomputer enthalten.

3. Aktivieren Sie das Kontrollkästchen **DirectAccess ausschließlich für mobile Computer aktivieren**, damit nur mobile Computer auf das interne Netzwerk zugreifen können.

4. Aktivieren Sie das Kontrollkästchen **Tunnelerzwingung verwenden**, um den gesamten Client-Datenverkehr (an das interne Netzwerk und das Internet) bei Bedarf über den Remotezugriffsserver zu leiten.

5. Klicken Sie auf **Weiter**.

## <a name="configure-the-network-topology"></a>Konfigurieren der Netzwerktopologie

Um den Remotezugriff bereitzustellen, müssen Sie den Remotezugriffsserver mit korrekten Netzwerkadaptern, einer öffentlichen URL für den Remotezugriffsserver, zu dem Clientcomputer eine Verbindung aufbauen können (die ConnectTo-Adresse), einem IP-HTTPS-Zertifikat mit einem Antragsteller, der mit der ConnectTo-Adresse übereinstimmt, konfigurieren.

1. Klicken Sie auf der Seite **Netzwerktopologie** auf die Bereitstellungstopologie, die in Ihrer Organisation verwendet wird. Geben Sie unter **Geben Sie den öffentlichen Namen oder die öffentliche IPv4-Adresse an** den öffentlichen Namen für die Bereitstellung ein (dieser Name stimmt mit dem Antragstellernamen des IP-HTTPS-Zertifikats überein, z. B. edge1.contoso.com), und klicken Sie dann auf **Weiter**.

## <a name="configure-the-dns-suffix-search-list"></a>Konfigurieren der Suchliste für DNS-Suffixe

Für DNS-Clients können Sie eine Suchliste für ein DNS-Domänensuffixe konfigurieren, die die DNS-Suchfunktionen erweitert oder überprüft. Indem Sie zusätzliche Suffixe zu der Liste hinzufügen, können Sie in mehreren angegebenen DNS-Domänen nach kurzen, nicht qualifizierten Computernamen suchen. Wenn eine DNS-Abfrage fehlschlägt, kann der DNS-Client Dienst diese Liste verwenden, um andere Namen Suffix-Endungen an ihren ursprünglichen Namen anzufügen und DNS-Abfragen für diese alternativen FQDNs an den DNS-Server zu wiederholen.

1. Wählen Sie **DirectAccess-Clients mit der Suchliste für DNS-Clientsuffixe konfigurieren**, um zusätzliche Suffixe für Clientnamen-Suchvorgänge anzugeben.

2. Geben Sie in **Neues Suffix** einen neuen Suffix ein, und klicken Sie dann auf **Hinzufügen**. Außerdem können Sie die Such Reihenfolge ändern und Suffixe aus **Domänen Suffixen entfernen, um Sie zu verwenden**.

>Nebenbei In einem Zusammenhang losen Namespace-Szenario, \( in dem ein oder mehrere Domänen Computer ein DNS-Suffix haben, das nicht der Active Directory Domäne entspricht, zu der die Computer gehören \) , sollten Sie sicherstellen, dass die Suchliste so angepasst ist, dass Sie alle erforderlichen Suffixe enthält. Der RAS-Assistent konfiguriert den Active Directory-DNS-Namen standardmäßig als primäres DNS-Suffix auf dem Client. Der Administrator sollte sicherstellen, dass er das von den Clients zur Namensauflösung verwendete DNS-Suffix hinzufügt.

Für Computer und Server ist das folgende standardmäßige DNS-Suchverhalten vorgegeben und wird verwendet, wenn kurze, nicht qualifizierte Namen vervollständigt und aufgelöst werden. Wenn die Suffixsuchliste leer oder nicht angegeben ist, wird das primäre DNS-Suffix des Computers an kurze, nicht qualifizierte Namen angehängt, und eine DNS-Abfrage wird verwendet, um den resultierenden FQDN aufzulösen.

Wenn bei der Abfrage ein Fehler auftritt, kann der Computer zusätzliche Abfragen für alternative voll qualifizierte Namen durchführen, indem ein beliebiges Verbindungs spezifisches DNS-Suffix angehängt wird, das für Netzwerkverbindungen konfiguriert ist. Wenn keine Verbindungs spezifischen Suffixe konfiguriert sind oder Abfragen für diese resultierenden Verbindungs spezifischen FQDNs fehlschlagen, kann der Client dann mit dem Wiederholen von Abfragen auf der Grundlage der systematischen Reduzierung des primären Suffixe (auch als "Devolution" bezeichnet) beginnen.

Wenn das primäre Suffix z. b. "example.Microsoft.com" ist, kann der Prozess der Verkürzung Abfragen für den Kurznamen wiederholen, indem er in den Domänen "Microsoft.com" und "com" danach sucht.

Wenn die Suffixsuchliste nicht leer ist und mindestens ein DNS-Suffix angegeben wurde, ist der Versuch, kurze DNS-Namen zu qualifizieren und aufzulösen, nur auf die durch die angegebene Suffixliste möglichen FQDNs beschränkt.

Wenn die Abfragen für alle durch das Anfügen und Versuchen der Suffixe in der Liste gebildeten FQDNs nicht aufgelöst werden können, schlägt der Abfragevorgang fehl und als Ergebnis wird "Name nicht gefunden" ausgegeben.

> [!WARNING]
> Wenn die Domänensuffixliste verwendet wird, senden die Clients weiterhin zusätzliche auf den verschiedenen DNS-Domänennamen basierende alternative Abfragen, wenn eine Abfrage nicht beantwortet oder aufgelöst wird. Nachdem ein Name mit einem Eintrag in der Suffixliste aufgelöst wurde, werden die nicht verwendeten Listeneinträge nicht versucht. Aus diesem Grund ist es am effizientesten, die Liste zunächst nach den am meisten verwendeten Domänensuffixen zu sortieren.
>
> Suchen nach Domänennamensuffixen werden nur verwendet, wenn ein DNS-Name nicht vollqualifiziert ist. Um einen DNS-Namen voll zu qualifizieren, müssen Sie am Ende des Namens einen nachstehenden Punkt (.) eingeben.

## <a name="gpo-configuration"></a>Konfiguration der Gruppenrichtlinienobjekte

Wenn Sie den Remote Zugriff konfigurieren, werden DirectAccess-Einstellungen in Gruppenrichtlinie Objekte (GPO) gesammelt.

Unter **GPO-Einstellungen**werden der Name des Gruppenrichtlinien Objekts für den DirectAccess-Server und der Name des Gruppenrichtlinien Objekts aufgeführt. Zusätzlich können Sie die GPO-Auswahleinstellungen ändern.

Zwei GPOs werden automatisch mit DirectAccess-Einstellungen aufgefüllt und auf diese Weise verteilt:

1. **DirectAccess-Client-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für die IPv6-Übergangstechnologie, der Einträge in der Richtlinientabelle für die Namensauflösung und der Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.

2. **DirectAccess-Server-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinien Objekt enthält die DirectAccess-Konfigurationseinstellungen, die auf jeden als RAS-Server konfigurierten Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.

## <a name="summary"></a>Zusammenfassung

Sobald die Konfiguration des Remote Zugriffs fertiggestellt ist, wird die **Zusammenfassung** angezeigt. Sie können die konfigurierten Einstellungen ändern oder auf **Fertig** stellen klicken, um die Konfiguration zu übernehmen.
