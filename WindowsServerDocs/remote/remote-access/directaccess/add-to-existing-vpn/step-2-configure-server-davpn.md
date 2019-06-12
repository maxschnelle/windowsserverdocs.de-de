---
title: Schritt 2 konfigurieren den DirectAccess-VPN-Server
description: Dieses Thema ist Teil des Handbuchs Add DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)-Bereitstellung für WindowsServer 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe221fc9-c7d9-4508-b8a1-000d2515283c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f8a6448661861fdc9f97c66fb130bfc03d0ce72c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446974"
---
#  <a name="step-2-configure-the-directaccess-vpn-server"></a>Schritt 2 konfigurieren den DirectAccess-VPN-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird die Konfiguration der Client- und Servereinstellungen erläutert, die für eine einfache Remotezugriffsbereitstellung mit dem Assistenten zum Aktivieren von DirectAccess erforderlich sind.

Die folgende Tabelle enthält eine Übersicht über die Schritte, die Sie mithilfe dieses Themas durchführen können.

|Aufgabe       |Beschreibung|
|-----------|-----------|
|Konfigurieren von DirectAccess-Clients|Konfigurieren Sie den Remotezugriffsserver mit den Sicherheitsgruppen, die die DirectAccess-Clients enthalten.|
|Konfigurieren der Netzwerktopologie|Konfigurieren Sie die Einstellungen des Remotezugriffsservers.|
|Konfigurieren der Suchliste für DNS-Suffixe|Ändern Sie die Suchliste für DNS-Suffixe bei Bedarf.|
|Konfiguration der Gruppenrichtlinienobjekte|Ändern Sie bei Bedarf die Gruppenrichtlinienobjekte.|

## <a name="to-start-the-enable-directacces-wizard"></a>So starten Sie den Assistenten zum Aktivieren von DirectAccess

1. Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **RAS**. Der Assistent zum Aktivieren von DirectAccess wird automatisch gestartet, es sei denn, die Sie ausgewählt haben **dieser Bildschirm nicht mehr anzeigen**. 

2. Wenn der Assistent nicht automatisch gestartet wird, mit der rechten Maustaste den Knoten für den Server in der Routing- und RAS-Struktur, und klicken Sie dann auf **Aktivieren von DirectAccess**.

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

Für DNS-Clients können Sie eine Suchliste für ein DNS-Domänensuffixe konfigurieren, die die DNS-Suchfunktionen erweitert oder überprüft. Indem Sie zusätzliche Suffixe zu der Liste hinzufügen, können Sie in mehreren angegebenen DNS-Domänen nach kurzen, nicht qualifizierten Computernamen suchen. Klicken Sie dann, wenn eine DNS-Abfrage ein Fehler auftritt, kann der DNS-Clientdienst diese Liste verwenden, fügen Sie andere Namen Suffix Zeilenenden auf Ihre ursprünglichen Namen, und wiederholen den DNS-Server DNS-Abfragen für diese alternativen FQDNs.

1. Wählen Sie **DirectAccess-Clients mit der Suchliste für DNS-Clientsuffixe konfigurieren**, um zusätzliche Suffixe für Clientnamen-Suchvorgänge anzugeben.

2. Geben Sie einen neuen Suffixnamen in **neues Suffix** , und klicken Sie dann auf **hinzufügen**. Darüber hinaus können Sie die Suchreihenfolge ändern und entfernen Sie die Suffixe aus **zu verwendende Domänensuffixe**.

>[HINWEIS] In einem zusammenhanglosen Namespace-Szenario \(, in denen eine oder mehrere Domänencomputer ein DNS-Suffix, das nicht zu dem die Computer gehören Active Directory-Domäne entspricht hat\), Sie sollten sicherstellen, dass die Suchliste angepasst wird, um alle der erforderlichen Suffixe. Der RAS-Assistent konfiguriert den Active Directory-DNS-Namen standardmäßig als primäres DNS-Suffix auf dem Client. Der Administrator sollte sicherstellen, dass er das von den Clients zur Namensauflösung verwendete DNS-Suffix hinzufügt.

Für Computer und Server wird der folgende DNS-Standardsuchverhalten vorbestimmt und beim Abschließen und Auflösen von kurzen, nicht qualifizierten Namen verwendet. Bei die Suffixsuchliste leer oder nicht angegeben ist, wird das primäre DNS-Suffix des Computers ist an kurze nicht qualifizierten Namen angehängt, und eine DNS-Abfrage wird verwendet, um den resultierenden FQDN aufzulösen. 

Wenn diese Abfrage fehlschlägt, kann der Computer zusätzliche Abfragen für alternativen FQDNs versuchen, durch Anfügen von einem verbindungsspezifischen DNS-Suffix für Netzwerkverbindungen konfiguriert. Wenn keine Verbindungsspezifische Suffixe konfiguriert sind, oder Abfragen für diese resultierende verbindungsspezifischen FQDNs nicht, wird der Client Abfragen basierend auf dem primären Suffix (auch bekannt als Verkürzung) systematische reduziert wiederholen anschließend beginnen kann.

Z. B. wenn das primäre Suffix "example.microsoft.com" ist, können die Verkürzung Abfragen für den kurzen Namen erneut nach einer Suche in der Domäne "microsoft.com" und "com".

Wenn der Suffixsuchliste Liste ist nicht leer und verfügt über mindestens ein DNS-Suffix angegeben wird, versucht, zu qualifizieren und kurze DNS-Namen aufzulösen, auf die Suche nur die FQDNs, die durch das der angegebenen Suffixliste beschränkt. 

Wenn die Abfragen für alle durch das Anfügen und Versuchen der Suffixe in der Liste gebildeten FQDNs nicht aufgelöst werden können, schlägt der Abfragevorgang fehl und als Ergebnis wird "Name nicht gefunden" ausgegeben. 

> [!WARNING]
> Wenn die Domänensuffixliste verwendet wird, senden die Clients weiterhin zusätzliche auf den verschiedenen DNS-Domänennamen basierende alternative Abfragen, wenn eine Abfrage nicht beantwortet oder aufgelöst wird. Nachdem ein Name mit einem Eintrag in der Suffixliste aufgelöst wurde, werden die nicht verwendeten Listeneinträge nicht versucht. Aus diesem Grund ist es am effizientesten, die Liste zunächst nach den am meisten verwendeten Domänensuffixen zu sortieren.
> 
> Suchen nach Domänennamensuffixen werden nur verwendet, wenn ein DNS-Name nicht vollqualifiziert ist. Um einen DNS-Namen voll zu qualifizieren, müssen Sie am Ende des Namens einen nachstehenden Punkt (.) eingeben.

## <a name="gpo-configuration"></a>Konfiguration der Gruppenrichtlinienobjekte

Wenn Sie Remotezugriff konfigurieren, werden die DirectAccess-Einstellungen in der Windows-Verwaltungsinstrumentation (Group Policy Objects, GPO) erfasst. 

In **GPO-Einstellungen**, die DirectAccess-Server-Gruppenrichtlinienobjekt-Namen und die Client-Gruppenrichtlinienobjektname aufgelistet sind. Zusätzlich können Sie die GPO-Auswahleinstellungen ändern.

Zwei Gruppenrichtlinienobjekte werden automatisch mit DirectAccess-Einstellungen aufgefüllt, und auf diese Weise verteilt:

1. **DirectAccess-Client-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die Client-Einstellungen, einschließlich der Einstellungen für die IPv6-Übergangstechnologie, der Einträge in der Richtlinientabelle für die Namensauflösung und der Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit. Das Gruppenrichtlinienobjekt wird auf die für die Clientcomputer angegebenen Sicherheitsgruppen angewendet.

2. **DirectAccess-Server-Gruppenrichtlinienobjekt**. Dieses Gruppenrichtlinienobjekt enthält die DirectAccess-Konfigurationseinstellungen, die auf den konfigurierten als RAS-Server in Ihrer Bereitstellung angewendet werden. Außerdem enthält es die Verbindungssicherheitsregeln für die Windows-Firewall mit erweiterter Sicherheit.

## <a name="summary"></a>Zusammenfassung

Sobald die Konfiguration des Remotezugriffs abgeschlossen ist. die **Zusammenfassung** wird angezeigt. Sie können die konfigurierten Einstellungen ändern, oder klicken Sie auf **Fertig stellen** zum Anwenden der Konfiguration.
