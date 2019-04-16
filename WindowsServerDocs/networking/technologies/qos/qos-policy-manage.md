---
title: Verwalten von QoS-Richtlinie
description: Dieses Thema enthält Anweisungen zum Erstellen und Verwalten von Quality of Service (QoS)-Richtlinie in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 04fdfa54-6600-43d4-8945-35f75e15275a
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5baa83e41c79a558f5bd32f77a234367726592c7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="manage-qos-policy"></a>Verwalten von QoS-Richtlinie

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können weitere Informationen zum Verwenden des Assistenten für die QoS-Richtlinie zum Erstellen, bearbeiten oder Löschen einer QoS-Richtlinie.

>[!NOTE]
>  Zusätzlich zu diesem Thema ist die folgende Dokumentation zum QoS-Richtlinie Verwaltung verfügbar.
> 
>  - [QoS-Richtlinie von Ereignissen und Fehlern](qos-policy-errors.md)

In Windows-Betriebssystemen werden QoS-Richtlinie die Funktionalität von standardbasiertem QoS mit der Verwaltbarkeit von Gruppenrichtlinien kombiniert. Konfiguration des diese Kombination ist eine einfache Anwendung von QoS-Richtlinien auf Gruppenrichtlinienobjekte. Windows enthält eine QoS-Richtlinie-Assistenten können Sie die folgenden Aufgaben ausführen.

-  [Erstellen einer QoS-Richtlinie](#bkmk_createpolicy)

-  [Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie](#bkmk_editpolicy)

##  <a name="bkmk_createpolicy"></a>Erstellen einer QoS-Richtlinie

Bevor Sie eine QoS-Richtlinie erstellen, ist es wichtig, dass Sie wissen, dass die beiden wichtigsten QoS-Steuerelemente, die verwendet werden, um den Netzwerkverkehr zu verwalten:

- DSCP-Wert

-   Drosselungsrate

### <a name="prioritizing-traffic-with-dscp"></a>Priorisierung von Datenverkehr mit DSCP-Markierung

Wie im vorherigen Anwendungsbeispiel Line-of-Business-bereits erwähnt, können Sie mithilfe die Priorität von ausgehendem Netzwerkdatenverkehr definieren **DSCP-Wert angeben** so konfigurieren Sie eine QoS-Richtlinie mit einem bestimmten DSCP-Wert. 

Wie Beschreibung in RFC 2474 ermöglicht DSCP Werte von 0 bis 63 im TOS-Feld IPv4-Pakets und im Feld Datenverkehrsklasse in IPv6 angegeben werden. Netzwerkrouter verwenden den DSCP-Wert, um Netzwerkpakete zu klassifizieren und sie entsprechend in die Warteschlange.
  
> [!NOTE]
>  Standardmäßig weist Windows Datenverkehr einen DSCP-Wert 0.
  
Die Anzahl der Warteschlangen und deren priorisierungsverhalten muss im Rahmen der QoS-Strategie Ihres Unternehmens entworfen werden. Ihrer Organisation können beispielsweise fünf Warteschlangen haben: wartezeitsensibler Datenverkehr, Steuerungsdatenverkehr, unternehmenskritische Datenverkehr, bestmöglichen Datenverkehr und Bulk-Datenübertragung Datenverkehr.  
  
### <a name="throttling-traffic"></a>Drosselung Datenverkehr

Zusammen mit DSCP-Werte ist die Einschränkung ein anderes Steuerelement zum Verwalten der Netzwerkbandbreite. Wie bereits erwähnt, können Sie die **Drosselungsrate angeben** Einstellung so konfigurieren Sie eine QoS-Richtlinie mit einer bestimmten Drosselungsrate für ausgehenden Datenverkehr. Mithilfe der Drosselung begrenzt eine QoS-Richtlinie den ausgehenden Netzwerkdatenverkehr zu einem angegebenen Drosselungsrate. DSCP-Markierung und Drosselung kann zusammen verwendet werden, um Datenverkehr effektiv zu verwalten.

>[!NOTE]
>Standardmäßig die **Drosselungsrate angeben** das Kontrollkästchen nicht aktiviert ist.

Um eine QoS-Richtlinie zu erstellen, bearbeiten Sie die Einstellungen von einem Gruppenrichtlinienobjekt (GPO) von innerhalb des Tools (Group Policy Management Console, GPMC). Gruppenrichtlinien-Verwaltungskonsole wird der Gruppenrichtlinien-Editor geöffnet.

QoS-Richtliniennamen müssen eindeutig sein. Anwenden von Richtlinien für Server und Endbenutzer, hängt davon ab, wo die QoS-Richtlinie im Gruppenrichtlinienobjekt-Editor gespeichert werden:

- Eine QoS-Richtlinie in Settings\QoS Computerkonfiguration\Windows-Richtlinie gilt für Computer, unabhängig von der Benutzer, der aktuell angemeldet ist. Normalerweise verwenden Sie computerbasierte QoS-Richtlinien für Servercomputer.

- Eine QoS-Richtlinie in die Benutzerrichtlinie Computerkonfiguration\Windows-Settings\QoS gilt für Benutzer, nach dem sie angemeldet sind unabhängig davon, welche, denen Computer sie angemeldet haben.

#### <a name="to-create-a-new-qos-policy-with-the-qos-policy-wizard"></a>So erstellen eine neue QoS-Richtlinie mit der QoS-Richtlinie-Assistenten

-   Gruppenrichtlinienobjekt-Editor mit der rechten Maustaste entweder von der **QoS-Richtlinie** Knoten, und klicken Sie dann auf **Erstellen einer neuen Richtlinie **.

### <a name="wizard-page-1---policy-profile"></a>Seite 1 - "Richtlinienprofil" des Assistenten

Auf der ersten Seite des Assistenten für QoS-Richtlinie können Sie einen Richtliniennamen angeben und konfigurieren, wie QoS ausgehenden Netzwerkdatenverkehr Steuerelemente.

#### <a name="to-configure-the-policy-profile-page-of-the-qos-based-policy-wizard"></a>So konfigurieren Sie die Seite "Richtlinienprofil" des Assistenten für richtlinienbasierten QoS

1. In **Richtlinienname**, geben Sie einen Namen für die QoS-Richtlinie. Der Name muss die Richtlinie eindeutig identifizieren.

2. Verwenden Sie optional **DSCP-Wert angeben** DSCP-Markierung zu aktivieren, und klicken Sie dann einen DSCP-Wert zwischen 0 und 63 zu konfigurieren.

3. Verwenden Sie optional **Drosselungsrate angeben** datenverkehrsdrosselung zu aktivieren und die Drosselungsrate zu konfigurieren. Wert der Drosselungsrate muss größer als 1 sein, und Sie können Einheiten Kilobytes pro Sekunde \(KBps\) oder Megabytes pro Sekunde \(MBps\) angeben.

4. Klicken Sie auf **Weiter**.

### <a name="wizard-page-2---application-name"></a>Seite 2 - Anwendungsname

In der zweiten Seite des Assistenten für QoS-Richtlinie können Sie die Richtlinie auf alle Anwendungen, auf eine bestimmte Anwendung anwenden, wie von den Programmname, um einen Pfad und Name der Anwendung oder auf die HTTP-Server-Anwendungen, die Behandlung von Anfragen für eine bestimmte URL ermittelt.

- **Alle Anwendungen** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie für alle Anwendungen gelten.

- **Nur Apps mit diesem Namen der ausführbaren Datei** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie für eine bestimmte Anwendung sind. Die ausführbare Datei benennen und mit der Erweiterung .exe enden.

- **Nur HTTP-Server-Anwendung reagiert auf Anforderungen für diese URL** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie auf bestimmten HTTP-Server-Anwendungen nur anwenden.

Optional können Sie den Anwendungspfad eingeben. Um eine Anwendungspfad anzugeben, geben Sie den Pfad mit den Namen der Anwendung ein. Der Pfad kann Umgebungsvariablen enthalten. Z.B. %ProgramFiles%\My Path\MyApp.exe oder c:\program files\my application path\myapp.exe.

>[!NOTE]
>Der Anwendungspfad kann nicht auf einen Pfad enthalten, der die eine symbolische Verknüpfung aufgelöst wird.

Die URL muss entsprechen [RFC 1738](http://tools.ietf.org/html/rfc1738), in Form von `http[s]://<hostname\>:<port\>/<url-path>`. Sie können einen Platzhalter verwenden, `‘*’`, für `<hostname>`und/oder `<port>`, z.B. `http://training.\*/, https://\*.\*`, aber die Platzhalter können keiner Teilzeichenfolge des `<hostname>`oder `<port>`.

Anders ausgedrückt, weder `http://my\*site/`noch `https://\*training\*/`gültig ist. 

Optional können Sie überprüfen, **Unterverzeichnisse und Dateien enthalten** auf alle Unterverzeichnisse und Dateien, die eine URL nach übereinstimmenden ausführen. Wenn diese Option aktiviert ist und die URL ist z.B. `http://training`, QoS-Richtlinie berücksichtigt die Anforderungen für` http://training/video` sehr gut geeignet.

#### <a name="to-configure-the-application-name-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Anwendungsname" des Assistenten für QoS-Richtlinie

1. In **diese QoS-Richtlinie gilt für**, wählen Sie entweder **alle Anwendungen** oder **nur Anwendungen mit diesem Namen der ausführbaren Datei **.

2. Wenn Sie die Option **nur Anwendungen mit diesem Namen der ausführbaren Datei**, geben Sie den Namen einer ausführbaren Datei mit der Erweiterung .exe.

3. Klicken Sie auf **Weiter**.

### <a name="wizard-page-3---ip-addresses"></a>Seite 3 – IP-Adressen

In der dritten Seite des Assistenten für QoS-Richtlinie können Sie die IP-Adresse Bedingungen für die QoS-Richtlinie, einschließlich der folgenden angeben:

- Alle Quell-IPv4- oder IPv6-Adressen oder bestimmte Quell-IPv4- oder IPv6-Adressen

- Alle Ziel-IPv4- oder IPv6-Adressen oder bestimmte Ziel-IPv4- oder IPv6-Adressen

Wenn Sie die Option **nur für die folgende Quell-IP-Adresse** oder **nur für die folgende Ziel-IP-Adresse**, müssen Sie Folgendes eingeben:

- Eine IPv4-Adresse, z.B. `192.168.1.1`

- IPv4-Adresspräfix mit Netzwerkpräfix-Längenschreibweise, wie `192.168.1.0/24`

- Eine IPv6-Adresse, z.B. `3ffe:ffff::1`

- Ein IPv6-Adresspräfix, z.B. `3ffe:ffff::/48`

Wenn Sie beide auswählen **nur für die folgende Quell-IP-Adresse** und **nur für die folgende Ziel-IP-Adresse**, Adressen oder Adresspräfixe muss entweder IPv4 oder IPv6-basierte.

Wenn Sie die URL für HTTP-Server-Anwendungen in der vorherigen Seite des Assistenten angegeben haben, werden Sie feststellen, dass die Quell-IP-Adresse für die QoS-Richtlinie auf dieser Seite des Assistenten deaktiviert ist. 

Dies gilt, da die Quell-IP-Adresse die HTTP-Server-Adresse wird ein, und es hier nicht konfigurierbar ist. Andererseits, können Sie die Richtlinie weiterhin anpassen, durch die Ziel-IP-Adresse angeben. Dadurch können Sie verschiedene Richtlinien für unterschiedliche Clients zu erstellen, indem Sie die gleichen HTTP-Server-Anwendungen.

#### <a name="to-configure-the-ip-addresses-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die IP-Adressen-Seite des Assistenten für QoS-Richtlinie

1. In **diese QoS-Richtlinie gilt für** (Quelle), wählen Sie **eine Quell-IP-Adresse** oder **nur für die folgenden IP-Quelladresse **.

2. Bei Auswahl von **nur die folgenden IP-Quelladresse**, geben Sie eine IPv4- oder IPv6-Adresse oder ein entsprechendes Präfix.

3. In **diese QoS-Richtlinie gilt für** (Ziel), wählen Sie **alle Zieladresse** oder **nur für die folgende Ziel-IP-Adresse.**

4. Bei Auswahl von **nur für die folgenden IP-Zieladresse**, eine IPv4- oder IPv6-Adresse oder ein Präfix, das den Typ der Adresse entspricht, oder das Präfix für die Quelladresse angegebenen anzugeben.

5.  Klicken Sie auf **Weiter**.  

### <a name="wizard-page-4---protocols-and-ports"></a>Assistentenseite für 4 - Protokolle und Ports

Auf der vierten Seite des Assistenten für QoS-Richtlinie können Sie angeben, die Typen von Netzwerkdatenverkehr und die Ports, die durch die Einstellungen auf der ersten Seite des Assistenten gesteuert werden. Sie können Folgendes angeben:  
-   TCP-Datenverkehr und/oder UDP-Datenverkehr  

-   Alle Quell-Ports, einen Quellportbereich oder einen bestimmten Quellport

-   Alle Zielports, einen Bereich von Zielports oder einen bestimmten Zielport  

#### <a name="to-configure-the-protocols-and-ports-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Protokolle und Ports" des Assistenten für QoS-Richtlinie

1. In **wählen Sie das Protokoll, das diese QoS-Richtlinie für gilt**Option **TCP**, **UDP**, oder **TCP- und UDP-**.

2. In **Geben Sie die Quellportnummer**Option **von einem beliebigen Quellport** oder **von dieser Quellportnummer **.

3. Bei Auswahl von **von dieser Quellportnummer**, geben Sie eine Zahl zwischen 1 und 65535.

     Optional können Sie einen Portbereich im Format angeben "*niedrig*:*hohe*,", in denen *niedrig* und *hohe* die einschließlichen unteren und oberen Begrenzungen des Portbereichs, einschließlich darstellen. *Niedrig* und *hohe* jede muss eine Zahl zwischen 1 und 65535 sein. Es darf kein Leerzeichen zwischen dem Doppelpunkt (:)) und den Zahlen.

4. In **Geben Sie die Zielportnummer**Option **an einen beliebigen Port** oder **an diese Zielportnummer**.

5. Bei Auswahl von **an diese Zielportnummer** Geben Sie im vorherigen Schritteine Portnummer zwischen 1 und 65535.

Klicken Sie zum Abschließen der Erstellung der neuen QoS-Richtlinie auf **Fertig stellen** auf die **Protokolle und Ports** Seite des Assistenten für QoS-Richtlinie. Wenn abgeschlossen ist, wird die neue QoS-Richtlinie im Detailbereich der Gruppenrichtlinien-Editor aufgeführt.  
  
Zum Anwenden der QoS-Richtlinieneinstellungen auf Benutzer oder Computer verknüpfen Sie das Gruppenrichtlinienobjekt in der QoS-Richtlinien mit einem Active Directory-Domänendienste-Container, z.B. einer Domäne, einer Website oder einer Organisationseinheit (OU) befinden.  
  
##  <a name="bkmk_editpolicy"></a>Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie

Die Seiten des Assistenten beschrieben die QoS-Richtlinie entsprechen den Eigenschaftenseiten, die angezeigt werden, wenn Sie anzeigen oder der Eigenschaften einer Richtlinie bearbeiten zuvor.  
  
### <a name="to-view-the-properties-of-a-qos-policy"></a>Anzeigen die Eigenschaften einer QoS-Richtlinie  
  
-   Maustaste auf den Richtliniennamen, klicken Sie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **Eigenschaften**.  
  
     Die Gruppenrichtlinien-Editor wird die Eigenschaftenseite mit den folgenden Registerkarten:  
  
    -   "Richtlinienprofil"  
  
    -   Anwendungsname  
  
    -   IP-Adressen  
  
    -   Protokolle und Ports  
  
### <a name="to-edit-a-qos-policy"></a>So bearbeiten Sie eine QoS-Richtlinie  
  
-   Maustaste auf den Richtliniennamen, klicken Sie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **vorhandene Richtlinie bearbeiten**.  
  
     Zeigt die Gruppenrichtlinien-Editors die **bearbeiten Sie eine vorhandene QoS-Richtlinie** Dialogfeld.  
  
### <a name="to-delete-a-qos-policy"></a>So löschen Sie eine QoS-Richtlinie  
  
-   Maustaste auf den Richtliniennamen, klicken Sie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **Richtlinie löschen**.  
  
### <a name="qos-policy-gpmc-reporting"></a>QoS-Richtlinie die Gruppenrichtlinien-Verwaltungskonsole Reporting 

Nachdem Sie eine Reihe von QoS-Richtlinien in Ihrer Organisation angewendet haben, kann es sein, hilfreich oder notwendig regelmäßig zu überprüfen, wie die Richtlinien angewendet werden. Eine Zusammenfassung der QoS-Richtlinien für einen bestimmten Benutzer oder Computer kann mithilfe der Gruppenrichtlinien-Verwaltungskonsole Berichte angezeigt werden.  
  
#### <a name="to-run-the-group-policy-results-wizard-for-a-report-of-qos-policies"></a>Zum Ausführen der Gruppenrichtlinienergebnis-Assistenten für einen Bericht von QoS-Richtlinien  
  
-   In der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste die **Gruppenrichtlinienergebnisse** Knoten, und wählen Sie dann im Menü die Option zum **Gruppenrichtlinienergebnis-Assistenten.**  
  
Nachdem der Gruppenrichtlinienergebnisse generiert werden, klicken Sie auf die **Einstellungen** Registerkarte. Auf der **Einstellungen** Registerkarte, die QoS-Richtlinien finden Sie unter "Computerkonfiguration\Windows Settings\QoS Richtlinie" und "Computerkonfiguration\Windows Settings\QoS Benutzerrichtlinie" Knoten.  
  
Auf der **Einstellungen** Registerkarte, die QoS-Richtlinien nach Namen QoS-Richtlinie mit ihren DSCP-Wert, Drosselungsrate, richtlinienbedingungen aufgeführt sind, und ausschlaggebenden Gruppenrichtlinienobjekt in der gleichen Zeile aufgeführt.  
  
Wird das ausschlaggebende Gruppenrichtlinienobjekt wird von der Gruppenrichtlinie Ergebnisansicht eindeutig identifiziert. Wenn mehrere Gruppenrichtlinienobjekte mit dem gleichen Namen der QoS-Richtlinie-QoS-Richtlinien verfügen, wird das Gruppenrichtlinienobjekt mit der höchsten Priorität Gruppenrichtlinienobjekt angewendet. Dies ist das ausschlaggebende Gruppenrichtlinienobjekt. In Konflikt stehende QoS-Richtlinien (gekennzeichnet durch Richtlinienname), die zugeordnet sind, um eine niedrigere Priorität Gruppenrichtlinienobjekt nicht angewendet werden. Beachten Sie, dass die GPO-Prioritäten zu definieren, welche QoS-Richtlinien in der Site, Domäne oder Organisationseinheit nach Bedarf bereitgestellt werden. Nach der Bereitstellung auf Benutzer oder Computer die [QoS-Richtlinie Rangfolgeregeln](#BKMK_precedencerules) feststellen, welcher Datenverkehr zulässig und blockiert wird.  
  
Der QoS-Richtlinie DSCP-Wert, Drosselungsrate und richtlinienbedingungen sind auch in Group Policy Objekt Editor (GPOE) sichtbar  
  
### <a name="advanced-settings-for-roaming-and-remote-users"></a>Erweiterte Einstellungen für Roaming und Remote-Benutzer  
QoS-Richtlinie geht es darum, die Verwaltung des Datenverkehrs im Netzwerk eines Unternehmens. In mobile Szenarien können Benutzer Datenverkehr aktivieren oder deaktivieren im Unternehmensnetzwerk senden. Da QoS-Richtlinien nicht von außerhalb des Unternehmens Netzwerk relevant sind, werden die QoS-Richtlinien nur auf Netzwerkschnittstellen aktiviert, die für Windows8, Windows7 oder Windows Vista für das Unternehmen verbunden sind.  
  
Beispielsweise kann ein Benutzer über ein Coffee Shop ihren tragbaren Computer mit ihrem Unternehmensnetzwerk über virtuelles privates Netzwerk (VPN) verbinden. Für VPN haben die physische Netzwerkschnittstelle (z.B. drahtlos) keinen QoS-Richtlinien angewendet. Allerdings müssen die VPN-Schnittstelle QoS-Richtlinien angewendet, da es für das Unternehmen eine Verbindung herstellt. Wenn der Benutzer später eine andere Unternehmensnetzwerk, die nicht über eine AD DS-Vertrauensstellung verfügt eingibt, werden die QoS-Richtlinien nicht aktiviert.  
  
Beachten Sie, dass diese mobile Szenarien nicht für serverarbeitsauslastungen gelten. Beispielsweise kann ein Server mit mehreren Netzwerkadaptern am Rand des Netzwerk eines Unternehmens befinden. Die IT-Abteilung kann festlegen, dass QoS-Richtlinien Drosselungsrate Datenverkehr, die das Unternehmen egresses; Diese Netzwerkadapter, die von diesen ausgehenden Datenverkehr gesendet wird jedoch nicht unbedingt wieder mit dem Unternehmensnetzwerk verbinden. Aus diesem Grund werden die QoS-Richtlinien immer auf alle Netzwerkschnittstellen eines Computers unter Windows Server2012 aktiviert.  
  
> [!NOTE]
>  Selektive Aktivierung gilt nur für QoS-Richtlinien und nicht für die erweiterte QoS-Einstellungen, die nachfolgend in diesem Dokument.  
  
### <a name="advanced-qos-settings"></a>Erweiterte QoS-Einstellungen

Erweiterte QoS-Einstellungen bieten zusätzliche Steuerelemente für IT-Administratoren zum Verwalten der Auslastung der Computer und DSCP-Kennzeichnungen. Erweiterte QoS-Einstellungen gelten nur auf dem Computer, während die QoS-Richtlinien auf die Computer und Benutzer angewendet werden können.

#### <a name="to-configure-advanced-qos-settings"></a>So konfigurieren Sie erweiterte QoS-Einstellungen

1.  Klicken Sie auf **Computerkonfiguration**, und klicken Sie dann auf **Windows-Einstellungen in der Gruppenrichtlinie**.
  
2.  Mit der rechten Maustaste **QoS-Richtlinie**, und klicken Sie dann auf **erweiterte QoS-Einstellungen**.

     Die folgende Abbildungzeigt die beiden erweiterte QoS-Einstellungen Registerkarten: **eingehender TCP-Datenverkehr** und **Markieren von DSCP-Markierung außer Kraft setzen**.
  
> [!NOTE]
>  Erweiterte QoS-Einstellungen werden auf Computerebene Group Policy Settings.
  
#### <a name="advanced-qos-settings-inbound-tcp-traffic"></a>Erweiterte QoS-Einstellungen: eingehender TCP-Datenverkehr

**Eingehender TCP-Datenverkehr** steuert der Auslastung der Netzwerkbandbreite TCP auf der Empfängerseite QoS-Richtlinien für den ausgehenden TCP und UDP-Datenverkehr nicht beeinträchtigen. 

Durch Festlegen eines geringeren Durchsatzes auf Ebene der **eingehender TCP-Datenverkehr** Registerkarte TCP schränkt die Größe der TCP-Empfangsfensters angekündigt. Die Auswirkung dieser Einstellung wird erhöhten Durchsatz und -Auslastung für TCP-Verbindungen mit höherer Bandbreiten oder Wartezeiten (Bandbreite Verzögerung Produkt) verknüpfen. Standardmäßig werden die maximalen Durchsatz auf Computern unter Windows Server2012, Windows8, Windows Server2008 R2, Windows Server2008 und Windows Vista fest.
  
Empfangene der TCP-Fenster in Windows Server2012, Windows8, Windows Server2008 R2, Windows Server2008 und Windows Vista aus früheren Versionen von Windows geändert hat. Frühere Versionen von Windows beschränkt der TCP-Fenster auf maximal 64 Kilobyte (KB), während die Windows Server2012, Windows8, Windows Server2008 R2, Windows Server2008 und Windows Vista dynamisch der Fenstergröße Receive-Side ändern bis zu 16 Megabyte (MB). In das Steuerelement für eingehenden TCP-Datenverkehr können Sie kontrollieren die eingehende Durchsatz durch Festlegen den maximalen Wert für den TCP-empfangen-Fenster gerecht werden. Die Ebenen entsprechen die folgenden Höchstwerte. 
  
|Eingehende Durchsatzlevel|Maximale|  
|------------------------|-------|  
|0|64KB|
|1|MINDESTENS 256KB|
|2|1MB|
|3|16MB|

Die tatsächliche Fenstergröße kann ein Wert kleiner als die maximal zulässige, je nach netzwerkbedingungen oder gleich sein.

###### <a name="to-set-the-tcp-receive-side-window"></a>Zum Festlegen des TCP-empfangsseitige

1. Klicken Sie im Gruppenrichtlinienobjekt-Editor auf **Richtlinie des lokalen Computers**, klicken Sie auf **Windows-Einstellungen**, klicken Sie mit der rechten Maustaste auf **QoS-Richtlinie**, und klicken Sie dann auf **erweiterte QoS-Einstellungen**.
  
2. In **empfangen Durchsatz von TCP-**Option **konfigurieren Sie TCP-empfangen Durchsatz**, und wählen Sie dann die Ebene der Durchsatz, die Sie möchten.

3.  Verknüpfen Sie das Gruppenrichtlinienobjekt mit der Organisationseinheit.

#### <a name="advanced-qos-settings-dscp-marking-override"></a>Erweiterte QoS-Einstellungen: DSCP markieren außer Kraft setzen.

Markieren von DSCP-Markierung außer Kraft setzen schränkt die Fähigkeit von Anwendungen an, oder "kennzeichnen" – DSCP-Werte als die in der QoS-Richtlinien. Durch die Angabe, dass Anwendungen DSCP-Werte festgelegt werden dürfen, können Anwendungen DSCP-Werte ungleich Null festlegen. 

Durch Angabe **ignorieren**, Anwendungen, die QoS-APIs verwenden, müssen ihre DSCP-Werte auf NULL gesetzt und QoS-Richtlinien können DSCP-Werte festlegen. 

Standardmäßig können Computern unter Windows Server2016, Windows10, Windows Server2012 R2, Windows8.1, Windows Server2012, Windows8, Windows Server2008 R2, Windows Server2008 und Windows Vista Anwendungen DSCP-Werte angegeben. Apps und Geräte, die nicht die QoS-APIs verwenden, werden nicht überschrieben.

##### <a name="wireless-multimedia-and-dscp-values"></a>Wireless Multimedia und DSCP-Werte

Die [Wi-Fi Alliance](https://go.microsoft.com/fwlink/?LinkId=160769) ergab eine Zertifizierung für Wireless Multimedia \(WMM\), die vier Kategorien definiert \(WMM_AC\) für die Priorisierung des Netzwerkdatenverkehrs in einem Drahtlosnetzwerk Wi\ WLAN übertragen. Die Kategorien gehören \ (in der Reihenfolge der höchsten zum niedrigsten Priority\): Stimme, Video, beste Aufwand und Hintergrund; als VO, VI, BE und BK bzw. abgekürzt. Die WMM-Spezifikation definiert, welche DSCP Werte entsprechen den vier Kategorien:
  
|DSCP-Wert|WMM Objektzugriff-Ereigniskategorie|
|----------|-------------------|
|48-63|Sprache (VO)|
|32-47|Video (VI)|
|24-31, 0-7|Beste Leistung (BE)|
|8-23|Hintergrund (s.)|

Sie können die QoS-Richtlinien erstellen, die diese DSCP-Werte verwenden, um sicherzustellen, dass tragbare Computer mit Wi\-Fi Certified™ für Drahtlosadapter WMM nach Priorität sortierten behandeln, wenn Wi\-Fi Certified WMM Zugriffspunkten zugeordnet sind.
  
### <a name="BKMK_precedencerules"></a>Rangfolgeregeln für QoS-Richtlinie

Ähnlich wie Gruppenrichtlinienobjekte Prioritäten, QoS-Richtlinien haben Vorrang vor Regeln zum Lösen von Konflikten, wenn mehrere QoS-Richtlinien auf eine bestimmte Gruppe von Datenverkehr anwenden. Für ausgehenden TCP- oder UDP-Datenverkehr kann nur eine QoS-Richtlinie zu einem Zeitpunkt angewendet werden, sodass QoS-Richtlinien nicht verfügen, dass ein kumulatives wirksam wird, z.B. wo Drosselungsrate Sätze zusammengefasst werden würde.

Im Allgemeinen gewinnt die QoS-Richtlinie mit den übereinstimmenden Bedingungen. Wenn mehrere QoS-Richtlinien anwenden, werden die Regeln in drei Kategorien fallen: Benutzerebene im Vergleich zu Computerebene; die Anwendung im Vergleich zu den Netzwerk-fünf Mal. und auf das Netzwerk quintuple.

Durch *Netzwerk Quintupel*, wir die Quell-IP-Adresse, Ziel-IP-Adresse, Quellport, Zielport bedeuten und \(TCP/UDP\)-Protokolls.  

 **QoS-Richtlinie auf Benutzerebene hat Vorrang vor Computerebene QoS-Richtlinie**

Diese Regel erleichtert erheblich Netzwerkadministratoren die Verwaltung von QoS-Gruppenrichtlinienobjekte, insbesondere für Benutzer-Richtlinien. Wenn beispielsweise der Netzwerkadministrator eine QoS-Richtlinie für eine Benutzergruppe definieren möchte, können sie einfach erstellen und verteilen ein Gruppenrichtlinienobjekts an diese Gruppe. Sie brauchen zu welchen, denen Computern Benutzer angemeldet sind und, ob diese Computer muss in Konflikt stehende QoS-Richtlinien definiert, da, wenn ein Konflikt besteht, die Richtlinie auf Benutzerebene immer Vorrang hat.

> [!NOTE]
>  Eine QoS-Richtlinie auf Benutzerebene gilt nur für den Datenverkehr, der von diesem Benutzer generiert wird. Andere Benutzer von einem bestimmten Computer und der Computer selbst, werden keine QoS-Richtlinien gelten, die für diesen Benutzer definiert werden.

 **Anwendung Genauigkeit und Vorrang vor den über fünf Mal Netzwerk**

Wenn mehrere QoS-Richtlinien für den Datenverkehr eines bestimmten übereinstimmen, wird die spezifischere Richtlinien angewendet. Zwischen den Richtlinien, die Anwendungen zu identifizieren, eine Richtlinie, die der sendenden Anwendung Dateipfad enthält detaillierter als eine andere Richtlinie gilt, die nur den Anwendungsnamen (ohne Pfad) identifiziert. Wenn mehrere Richtlinien mit Anwendungen weiterhin anwenden, verwenden die Rangfolgeregeln Quintupel Netzwerk nach der besten Übereinstimmung.

Alternativ können mehrere QoS-Richtlinien für den gleichen Datenverkehr anwenden, indem übereinander Bedingungen angeben. Zwischen der Garantien in Bezug auf Anwendungen und das Netzwerk fünf Mal die Richtlinie, die in der Anwendung wird gilt spezifischere und angewendet wird. 

Z.B. Policy_A gibt nur eine Anwendung Namen (App.exe) und Policy_B gibt die Ziel-IP-Adresse 192.168.1.0/24. Wenn diese QoS-Richtlinien in Konflikt \ (App.exe sendet Datenverkehr an eine IP-Adresse innerhalb des Bereichs der 192.168.4.0/24\), wird das Policy_A angewendet.

 **Weitere Genauigkeit Vorrang innerhalb des Netzwerks Quintupel**

Für Richtlinienkonflikte in das Netzwerk fünf Mal Vorrang die Richtlinie mit den meisten übereinstimmenden Bedingungen. Nehmen wir beispielsweise an, dass Policy_C gibt Quell-IP-Adresse "Beliebig", Ziel-IP-Adresse 10.0.0.1, Quellport "any" Zielport "alle" und "TCP"-Protokoll. 

Als Nächstes wird davon ausgegangen Sie, dass Policy_D gibt Quell-IP-Adresse "Beliebig", Ziel-IP-Adresse 10.0.0.1, Quellport "any" Zielport 80 und Protokoll "TCP". Klicken Sie dann mit Policy_C und Policy_D Verbindungen mit Ziel 10.0.0.1:80 übereinstimmen. Da QoS-Richtlinie die Richtlinie mit den genauesten übereinstimmenden Bedingungen anwendet, Vorrang Policy_D in diesem Beispiel.  
  
Jedoch möglicherweise die QoS-Richtlinien für die gleiche Anzahl von Bedingungen. Mehrere Richtlinien können jede Geben Sie z.B. nur eine (aber nicht identisch) Teil der Netzwerk-fünf Mal. Zwischen den fünf Mal Netzwerk wird der folgende Reihenfolge von höherer Rangfolge senken:

- Quell-IP-Adresse

- Ziel-IP-Adresse

- Quellport

- Zielport

- Protokoll (TCP oder UDP)

Innerhalb einer bestimmten Bedingung, z.B. IP-Adresse wird eine spezifische IP-Adresse mit höherer Priorität behandelt. Beispielsweise ist eine IP-Adresse 192.168.4.1 genauer als 192.168.4.0/24.

Entwerfen Sie Ihre QoS-Richtlinien möglichst genau wie möglich zur Vereinfachung Ihrer Organisation die Möglichkeit, zu verstehen, welche Richtlinien in Kraft sind.

Im nächsten Thema in diesem Handbuch, finden Sie unter [QoS-Richtlinie von Ereignissen und Fehlern](qos-policy-errors.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
