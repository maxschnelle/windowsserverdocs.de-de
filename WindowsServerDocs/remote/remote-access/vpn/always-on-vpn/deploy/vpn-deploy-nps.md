---
title: Installieren und Konfigurieren von NPS-Servers
description: NPS-Server-Verarbeitung von verbindungsanforderungen, die der VPN-Server gesendet werden überprüft, ob der Benutzer über die Berechtigung für die Verbindung, die Identität des Benutzers, verfügt und protokolliert die Aspekten der Anforderung der Verbindung, die Sie ausgewählt haben, wenn Sie RADIUS-Kontoführung in NPS konfiguriert haben.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: ca53ef28497a78f264c60ac1132f721fb6e01c15
ms.sourcegitcommit: 9c142ad4d4321baf328707f29fa104247ff5149a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "9035766"
---
# Schritt 4. Installieren und Konfigurieren von Netzwerkrichtlinienserver (Network Policy Server, NPS)

>   Gilt für: WindowsServer 2019, WindowsServer (Semi-Annual Channel), WindowsServer 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **Weiter:** Schritt 3. Konfigurieren Sie die RAS-Servers für Always On VPN](vpn-deploy-ras.md)<br>
& #187;  [ **Weiter:** Schritt 5. Konfigurieren von DNS und Firewall-Einstellungen](vpn-deploy-dns-firewall.md)


In diesem Schritt installieren Sie Netzwerkrichtlinienserver (Network Policy Server, NPS) für die Verarbeitung von verbindungsanforderungen, die der VPN-Server gesendet werden:

- Führen Sie die Autorisierung, um sicherzustellen, dass der Benutzer eine Zugriffsberechtigung für die Verbindung hat.
- Durchführen der Authentifizierung, um die Identität des Benutzers zu überprüfen.
- Ausführen von Kontoführung, um die Aspekte der Anforderung der Verbindung zu protokollieren, die Sie ausgewählt haben, wenn Sie RADIUS-Kontoführung in NPS konfiguriert haben.

Die Schritte in diesem Abschnitt können Sie die folgenden Aufgaben auszuführen:

1.  Auf dem Computer oder virtuellen Computer, die für den Netzwerkrichtlinienserver geplant und auf Ihr Unternehmen oder Ihre Unternehmensnetzwerk installiert, können Sie NPS installieren.

   >[!TIP] 
   >Wenn Sie bereits eine oder mehrere NPS-Servern in Ihrem Netzwerk verfügen, müssen Sie nicht NPS-Servers installieren – stattdessen können Sie in diesem Thema verwenden, um die Konfiguration eines vorhandenen NPS-Servers zu aktualisieren.

>[!NOTE]  
Sie können den Netzwerkrichtlinienserver-Dienst nicht unter Windows Server Core installieren.

2.  Auf der Organisation/Unternehmens NPS-Servers können Sie NPS als RADIUS-Server ausführen, die die verbindungsanforderungen, die von der VPN-Server empfangen verarbeitet konfigurieren.

## Installieren des Netzwerkrichtlinienservers

In diesem Verfahren installieren Sie NPS mithilfe von Windows PowerShell oder die Manager Hinzufügen von Serverrollen und Features-Assistenten. NPS ist ein Rollendienst der Network Policy and Access Services-Serverrolle.

>[!TIP] 
>Standardmäßig überwacht NPS RADIUS-Datenverkehr auf Ports 1812, 1813, 1645 und 1646 auf alle installierten Netzwerkadapter. Wenn Sie von NPS installieren, und die Windows-Firewall mit erweiterter Sicherheit aktivieren, erhalten Firewallausnahmen für diese Ports für IPv4 und IPv6-Datenverkehr automatisch erstellt. Wenn Server für den Netzwerkzugriff zum Senden von RADIUS-Datenverkehr über Ports als diese Standardwerte konfiguriert sind, entfernen Sie die Ausnahmen, die in Windows-Firewall mit erweiterter Sicherheit während der Installation von NPS erstellt haben, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Datenverkehr.

**Verfahren für Windows PowerShell:**

Zum Ausführen dieser Schritte mithilfe von Windows PowerShell, führen Sie Windows PowerShell als Administrator, geben Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE.

`Install-WindowsFeature NPAS -IncludeManagementTools`

**Schritt für Server-Manager:**

1.  Klicken Sie im Server-Manager auf **Verwalten**, und klicken Sie auf **Hinzufügen von Rollen und Features**. <p>Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  Klicken Sie bevor Sie beginnen auf **Weiter**.

    >[!NOTE] 
    >Die Seite " **Vorbereitung** " des Hinzufügen von Rollen und Features-Assistenten wird nicht angezeigt, wenn Sie vorher **Seite standardmäßig überspringen** , beim Hinzufügen von Rollen und Features-Assistenten ausführen ausgewählt haben.

1.  Select Installation Type sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie auf **Weiter**.

2.  Zielserver auswählen stellen Sie sicher, dass **einen Server aus dem Serverpool auswählen** aktiviert ist.

3.  Stellen Sie im Server-Pool sicher, dass der lokale Computer ausgewählt ist, und klicken Sie auf **Weiter**.

4.  Wählen Sie im Serverrollen auswählen, **Rollen** **Network Policy and Access Services**. Ein Dialogfeld gefragt werden, ob diese Funktionen für Network Policy and Access Services hinzufügen sollten.

5.  Klicken Sie auf **Features hinzufügen**, und klicken Sie auf **Weiter**

6.  Select Features klicken Sie auf **Weiter**in Network Policy and Access Services, überprüfen Sie die bereitgestellten Informationen und klicken Sie auf **Weiter**.

7.  Klicken Sie im wählen Rollendienste auf **Network Policy Server**.

8.  Klicken Sie für Funktionen für Network Policy Server auf **Features hinzufügen** , und klicken Sie auf **Weiter**.

9.  Installationsauswahl bestätigen klicken Sie auf **den Zielserver neu starten, automatisch, wenn erforderlich**.

10. Klicken Sie auf **Ja,** um die ausgewählten zu bestätigen, und klicken Sie dann auf **Installieren**. <p>Die Seite "Installation Progress" zeigt den Status während der Installation. Wenn der Vorgang abgeschlossen ist, wird die Meldung "Installation auf *ComputerName*war erfolgreich" angezeigt, in denen *ComputerName* der Name des Computers ist, auf dem Sie Network Policy Server installiert.

11. Klicken Sie auf **Schließen**.

## Konfigurieren von NPS

Von der VPN-Server empfängt, nach dem Installieren von NPS, Sie Konfigurieren von NPS zum behandeln alle Authentifizierung, Autorisierung und Kontoführung Aufgaben für Verbindung anfordern.

### Registrieren des Netzwerkrichtlinienservers in Active Directory

In diesem Verfahren registrieren Sie den Server in Active Directory, sodass es Zugriffsberechtigung für Benutzerkontoinformationen während der Verarbeitung von verbindungsanforderungen hat.

**Verfahren:**

1.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Network Policy Server**. Die NPS-Konsole wird geöffnet.

2.  Klicken Sie in der NPS-Konsole mit der rechten Maustaste **NPS (lokal)**, und klicken Sie auf **Server in Active Directory registrieren** , um es auszuwählen.<p>Das Dialogfeld Network Policy Server wird geöffnet.

3.  Klicken Sie im Dialogfeld Network Policy Server zweimal auf **OK** .

Alternativer Methoden für die Registrierung von NPS finden Sie in der [Registrierung eines NPS-Servers in einer Active Directory-Domäne](../../../../../networking/technologies/nps/nps-manage-register.md).

### Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

Konfigurieren Sie in diesem Verfahren-Netzwerk-Richtlinie Server-Kontoführung mithilfe einer der folgenden Protokollierung Typen:

-   Das **Ereignis protokolliert**. Wird in erster Linie für die Überwachung und Problembehandlung von versucht, eine Verbindung verwendet. Sie können NPS-Protokollierung erhalten Sie die NPS-Server-Eigenschaften in der NPS-Konsole konfigurieren.

-   **Protokollierung Benutzerauthentifizierung und Kontoführung Anforderungen in einer lokalen Datei**. Wird in erster Linie für Verbindung Analyse und Abrechnung verwendet. Auch verwendet als ein Sicherheit Untersuchung-Tool, da Sie eine Methode für die Aktivität ein böswilliger Benutzer nach einem Angriff nachverfolgen erhalten. Sie können mit dem Assistenten für Buchhaltung lokale Datei Protokollierung konfigurieren.

-   Die **Benutzerauthentifizierung und Kontoführung Anfragen in einer Microsoft SQL Server-XML-kompatiblen Datenbank protokolliert**. Verwendung von mehreren Servern mit NPS auf eine Datenquelle verfügen. Außerdem bietet die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server-Protokollierung konfigurieren, indem Sie mit dem Assistenten für Buchhaltung.

Um Network Policy Server-Kontoführung zu konfigurieren, finden Sie unter [Konfigurieren Network Policy Server Buchhaltung](../../../../../networking/technologies/nps/nps-accounting-configure.md).

### Der VPN-Server als RADIUS-Client hinzu

Im Abschnitt [Konfigurieren des RAS-Servers für Always On VPN](vpn-deploy-ras.md) installiert und konfiguriert den VPN-Server. Bei der VPN-Server-Konfiguration haben Sie einen gemeinsamen geheimen RADIUS-Schlüssel auf dem VPN-Server hinzugefügt. 

In diesem Verfahren verwenden Sie die gleichen freigegebenen geheimen Textzeichenfolge zum Konfigurieren des VPN-Servers als RADIUS-Client in NPS. Verwenden Sie die gleichen Textzeichenfolgen, die Sie auf dem VPN-Server verwendet, oder die Kommunikation zwischen dem NPS-Servers und der VPN-Server schlägt fehl.

>[!IMPORTANT] 
>Wenn Sie neue Netzwerkserver (VPN-Server, Drahtloszugriffspunkts, authentifizierende Switch oder DFÜ-Server) mit dem Netzwerk hinzufügen, müssen Sie den Server als RADIUS-Client in NPS hinzufügen, sodass NPS im Hinblick auf und mit Network Access Server kommunizieren kann.

**Verfahren:**

1.  Doppelklicken Sie auf dem Netzwerkrichtlinienserver, in der NPS-Konsole auf **RADIUS-Clients und Servern**.

2.  Mit der rechten Maustaste **RADIUS-Clients** , und klicken Sie auf **neu**. Das Dialogfeld Neuer RADIUS-Client geöffnet wird.

3.  Stellen Sie sicher, dass das Kontrollkästchen **Aktivieren dieser RADIUS-Client** aktiviert ist.

4.  **Anzeigename**Geben Sie einen Anzeigenamen für den VPN-Server.

5.  Geben Sie in **die Adresse (IP oder DNS)** die NAS-IP-Adresse oder den FQDN.<p>Wenn Sie den FQDN eingeben, klicken Sie auf **Überprüfen** , wenn Sie möchten, um sicherzustellen, dass der Name korrekt ist und in eine gültige IP-Adresse zugeordnet ist.

6.  **Gemeinsamer geheimer Schlüssel**führen Sie:

    1.  Stellen Sie sicher, dass **manuell** aktiviert ist.

    2.  Geben Sie eine sichere Zeichenfolge, die Sie auch auf dem VPN-Server eingegeben haben.

    3.  Geben Sie den gemeinsamen geheimen Schlüssel in gemeinsamen geheimen Schlüssel bestätigen.

7.  Klicken Sie auf **OK**. Der VPN-Server wird in der Liste der RADIUS-Clients, die auf dem Netzwerkrichtlinienserver konfiguriert angezeigt.

## Konfigurieren von NPS als RADIUS für VPN-Verbindungen

In diesem Verfahren konfigurieren Sie NPS als RADIUS-Server im Netzwerk Ihrer Organisation. Für den NPS, müssen Sie eine Richtlinie, die nur für Benutzer in der Organisation/Unternehmensnetzwerk über die VPN-Server - Zugriff auf eine bestimmte Gruppe ermöglicht definieren und dann nur, wenn Sie ein gültiges Benutzerzertifikat in eine Anforderung der PEAP-Authentifizierung verwenden.

**Verfahren:**

1.  In der NPS-Konsole Standardkonfiguration stellen Sie sicher, dass **RADIUS-Server für DFÜ- oder VPN-Verbindungen** aktiviert ist.

2.  Klicken Sie auf **VPN oder DFÜ - konfigurieren**.<p>Das VPN konfigurieren oder DFÜ-Assistent wird geöffnet.

3.  Klicken Sie auf **Virtual Private Network (VPN)-Verbindungen**, und klicken Sie auf **Weiter**.

4.  Wählen Sie im angeben DFÜ- oder VPN-Server in RADIUS-Clients der Name des der VPN-Server, die Sie im vorherigen Schritt hinzugefügt.<p>Beispielsweise ist der VPN-Server NetBIOS-Namen RAS1, klicken Sie auf **RAS1**.

5.  Klicken Sie auf **Weiter**.

6.  Führen Sie in konfiguriert Authentifizierungsmethoden zu verwenden die folgenden Schritte aus:

    1.  Deaktivieren Sie das Kontrollkästchen **Microsoft-verschlüsselte Authentifizierung, Version 2 (MS-CHAPv2)** .

    2.  Klicken Sie auf das Kontrollkästchen **Extensible Authentication-Protokoll** , um es auszuwählen.

    3.  Klicken Sie im-Typ (basierend auf der Methode der Zugriff und Netzwerkkonfiguration) auf **Microsoft: geschütztes EAP (PEAP)**, und klicken Sie auf **Konfigurieren**.<p>Das Dialogfeld "Eigenschaften für geschütztes EAP bearbeiten" wird geöffnet.

    4.  Klicken Sie auf **Entfernen** , um den EAP-Typ für sicheres Kennwort (EAP-MSCHAP v2) zu entfernen.

    5.  Klicken Sie auf **Hinzufügen**. Das Dialogfeld EAP hinzufügen wird geöffnet.

    6.  Klicken Sie auf **Smartcard oder anderes Zertifikat**, und klicken Sie auf **OK**.

    7.  Klicken Sie auf **OK** , um Eigenschaften für geschütztes EAP bearbeiten zu schließen.

7.  Klicken Sie auf **Weiter**.

8.  Führen Sie in Benutzergruppen angeben die folgenden Schritte aus:

    1.  Klicken Sie auf **Hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Computern, Dienstkonten oder Gruppen wird geöffnet.

    2.  Geben Sie die **VPN-Benutzer** , und klicken Sie auf **OK**.

    3.  Klicken Sie auf **Weiter**.

9.  Geben Sie IP-Filter klicken Sie auf **Weiter**.

10. Klicken Sie unter "Einstellungen" angeben, Verschlüsselung auf " **Weiter**". Machen Sie keine Änderungen.<p>Diese Einstellungen gelten nur für Microsoft-Punkt-Verschlüsselung (MPPE)-Verbindungen, die in diesem Szenario nicht unterstützt.

11. Geben Sie einen Bereichsnamen ein Klicken Sie auf **Weiter**.

12. Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen.

## Zertifikat nicht registrieren NPS-Servers

In diesem Verfahren aktualisieren Sie Gruppenrichtlinien auf dem lokalen Netzwerkrichtlinienserver manuell. Wenn automatisch registriert Gruppenrichtlinien aktualisiert, wenn die automatische Registrierung von Zertifikaten ist konfiguriert ist und ordnungsgemäß funktioniert, der lokale Computer ein Zertifikat von der Zertifizierungsstelle (CA).

>[!NOTE]  
>Gruppenrichtlinien werden automatisch aktualisiert, wenn Sie die Domänenmitgliedscomputer neu starten, oder wenn ein Benutzer auf einem Domänenmitgliedscomputer anmeldet. Darüber hinaus wird in regelmäßigen Abständen Gruppenrichtlinien aktualisiert. Standardmäßig erfolgt diese regelmäßige Aktualisierung alle 90 Minuten mit einem zufälligen Versatz von bis zu 30 Minuten.

Mitgliedschaft in **Administratoren**oder einer entsprechenden, ist die Mindestanforderungen zum Ausführen dieses Vorgangs.

**Verfahren:**

1.  Öffnen Sie auf der NPS Windows PowerShell.

2.  Geben Sie in der Windows PowerShell-Eingabeaufforderung **Gpupdate**, und drücken Sie die EINGABETASTE.

## Nächster Schritt
[Schritt 5. Konfigurieren von DNS und Firewall-Einstellungen für Always On VPN](vpn-deploy-dns-firewall.md): In diesem Schritt Sie Netzwerkrichtlinienserver (Network Policy Server, NPS) mithilfe von Windows PowerShell oder die Manager Hinzufügen von Serverrollen und Features Assistenten installieren. Sie auch Konfigurieren von NPS zum behandeln alle Authentifizierung, Autorisierung und Kontoführung Aufgaben für Verbindung Anforderungen, die sie aus der VPN-Server empfängt.



---

