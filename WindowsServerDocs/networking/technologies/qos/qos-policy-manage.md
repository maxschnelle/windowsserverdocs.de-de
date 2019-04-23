---
title: Verwalten von QoS-Richtlinie
description: Dieses Thema enthält Anweisungen zum Erstellen und Verwalten von Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 04fdfa54-6600-43d4-8945-35f75e15275a
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 94e5a1832a6c1e160b9cc338d50636026a5eb751
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851671"
---
# <a name="manage-qos-policy"></a>Verwalten von QoS-Richtlinie

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um zu erfahren, mit dem Assistenten für die QoS-Richtlinie erstellen, bearbeiten oder Löschen einer QoS-Richtlinie.

>[!NOTE]
>  Zusätzlich zu diesem Thema steht die folgende Dokumentation zum Management von QoS-Richtlinie.
> 
>  - [QoS-Richtlinie-Ereignisse und-Fehler](qos-policy-errors.md)

In Windows-Betriebssystemen kombiniert die QoS-Richtlinie die Funktionalität von standardbasiertem QoS mit der Verwaltbarkeit von Gruppenrichtlinien. Konfiguration des diese Kombination ist eine einfache Anwendung von QoS-Richtlinien auf Gruppenrichtlinienobjekte. Windows enthält einen Assistenten QoS-Richtlinie, damit Sie die folgenden Aufgaben ausführen können.

-  [Erstellen Sie eine QoS-Richtlinie](#bkmk_createpolicy)

-  [Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie](#bkmk_editpolicy)

##  <a name="bkmk_createpolicy"></a>Erstellen Sie eine QoS-Richtlinie

Bevor Sie eine QoS-Richtlinie erstellen, ist es wichtig, dass Sie verstehen, dass die beiden wichtigsten QoS-Steuerelemente, die verwendet werden, um den Netzwerkverkehr zu verwalten:

- DSCP-Wert

-   Drosselungsrate

### <a name="prioritizing-traffic-with-dscp"></a>Priorisieren des Datenverkehrs mit DSCP

Wie im vorherigen Anwendungsbeispiel Line-of-Business-erwähnt, können Sie die Priorität des ausgehenden Netzwerkdatenverkehrs definieren, indem Sie mithilfe von **DSCP-Wert angeben** so konfigurieren Sie eine QoS-Richtlinie mit einem bestimmten DSCP-Wert. 

Wie der Beschreibung in RFC 2474 ermöglicht DSCP das Werte von 0 bis 63 innerhalb des TOS-Felds eines IPv4-Pakets und innerhalb des Traffic Class-Felds in IPv6 angegeben werden. Netzwerkrouter verwenden den DSCP-Wert, um Netzwerkpakete zu klassifizieren und diese ordnungsgemäß in die Warteschlange.
  
> [!NOTE]
>  Standardmäßig hat die Windows-Datenverkehr einen DSCP-Wert 0.
  
Die Anzahl der Warteschlangen und deren Priorisierungsverhalten muss im Rahmen der QoS-Strategie der Organisation festgelegt werden. Z. B. Ihrer Organisation können fünf Warteschlangen: wartezeitempfindlichem Datenverkehr, Steuerungsdatenverkehr, geschäftskritische Datenverkehr, Best-Effort-Prinzip Datenverkehr und Massendatenübertragung Datenverkehr.  
  
### <a name="throttling-traffic"></a>Drosseln des Datenverkehrs

Zusammen mit DSCP-Werten ist die Einschränkung einen anderen-Steuerelements für die Verwaltung der Netzwerkbandbreite. Wie bereits erwähnt, können Sie die **Drosselungsrate angeben** Einstellung, um eine QoS-Richtlinie mit einer bestimmten Drosselungsrate für ausgehenden Datenverkehr konfigurieren. Mithilfe der Drosselung begrenzt eine QoS-Richtlinie den ausgehenden Netzwerkdatenverkehr zu einer angegebenen Drosselungsrate. DSCP-Markierung und Drosselung können gemeinsam verwendet werden, um den Datenverkehr effektiv zu verwalten.

>[!NOTE]
>Das Kontrollkästchen **Drosselungsrate angeben** ist standardmäßig nicht aktiviert.

Um eine QoS-Richtlinie zu erstellen, bearbeiten Sie die Einstellungen von einer Gruppe Gruppenrichtlinienobjekt (GPO) von innerhalb des Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC)-Tools. Gruppenrichtlinien-Verwaltungskonsole wird der Gruppenrichtlinienobjekt-Editor wird geöffnet.

QoS-Richtliniennamen müssen eindeutig sein. Zum Anwenden von Richtlinien auf Servern und Endbenutzern, hängt davon ab, wo die QoS-Richtlinie in der Gruppenrichtlinienobjekt-Editor gespeichert werden:

- Eine QoS-Richtlinie in Settings\QoS Computerkonfiguration\Windows-Richtlinie gilt für Computer, unabhängig vom Benutzer, der zurzeit angemeldet ist. Normalerweise verwenden Sie computerbasierte QoS-Richtlinien für Servercomputer.

- Eine QoS-Richtlinie in User Configuration\Windows Settings\QoS Richtlinie gilt für Benutzer, nachdem sie angemeldet sind unabhängig davon, welche, denen Computer sie sich angemeldet haben.

#### <a name="to-create-a-new-qos-policy-with-the-qos-policy-wizard"></a>Erstellen Sie eine neue QoS-Richtlinie mit dem Assistenten für QoS-Richtlinie

-   Im Gruppenrichtlinienobjekt-Editor, mit der rechten Maustaste entweder von der **QoS-Richtlinie** Knoten, und klicken Sie dann auf **Erstellen einer neuen Richtlinie**.

### <a name="wizard-page-1---policy-profile"></a>Assistentenseite 1: "Richtlinienprofil"

Auf der ersten Seite des Assistenten für QoS-Richtlinie können Sie einen Richtliniennamen angeben und konfigurieren, wie QoS für ausgehenden Netzwerkdatenverkehr steuert.

#### <a name="to-configure-the-policy-profile-page-of-the-qos-based-policy-wizard"></a>So konfigurieren Sie die Seite "Richtlinienprofil" des Assistenten für richtlinienbasierten QoS

1. Geben Sie in das Feld **Richtlinienname** einen Namen für die QoS-Richtlinie ein. Der Name muss die Richtlinie eindeutig identifizieren.

2. Verwenden Sie optional **DSCP-Wert angeben** DSCP-Markierung zu aktivieren, und klicken Sie dann einen DSCP-Wert zwischen 0 und 63 zu konfigurieren.

3. Verwenden Sie optional **Drosselungsrate angeben**, um die Datenverkehrsdrosselung zu aktivieren und die Drosselungsrate zu konfigurieren. Wert der Drosselungsrate muss größer als 1 sein, und Sie können Einheiten von Kilobytes pro Sekunde angeben \(Kbit/s\) oder Megabytes pro Sekunde \(Mbit/s\).

4. Klicken Sie auf **Weiter**.

### <a name="wizard-page-2---application-name"></a>Assistentenseite 2 - Anwendungsname

In der zweiten Seite des Assistenten für QoS-Richtlinie können Sie die Richtlinie auf alle Anwendungen, die an eine bestimmte Anwendung anwenden, das mit seinem ausführbaren Datei, in einen Pfad und Name der Anwendung oder den HTTP-serveranwendungen, die Anforderungen für eine bestimmte URL zu verarbeiten.

- **Alle Anwendungen** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie für alle dienstanwendungen gelten.

- **Nur Anwendungen mit dieser ausführbaren Datei** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie für eine bestimmte Anwendung. Der Name der ausführbaren Datei muss die Dateinamenerweiterung EXE aufweisen.

- **Nur HTTP-Server-Anwendungen reagieren auf Anforderungen für diese URL** gibt an, dass die Einstellungen für die datenverkehrsverwaltung auf der ersten Seite des Assistenten für QoS-Richtlinie auf bestimmte HTTP-Server-Anwendungen nur anzuwenden.

Optional können Sie den Anwendungspfad eingeben. Zum Angeben des Anwendungspfads geben Sie den Pfad zusammen mit dem Anwendungsnamen ein. Der Pfad kann Umgebungsvariablen enthalten. Beispiele: "%ProgramFiles%\Mein Anwendungspfad\MeineAnwendung.exe" oder "C:\Programme\Mein Anwendungspfad\MeineAnwendung.exe".

>[!NOTE]
>Der Pfad der Anwendung kann nicht auf einen Pfad enthalten, der die eine symbolische Verknüpfung aufgelöst wird.

Die URL muss entsprechen [RFC 1738](https://tools.ietf.org/html/rfc1738), in Form von `http[s]://<hostname\>:<port\>/<url-path>`. Sie können einen Platzhalter verwenden, `‘*’`, für `<hostname>` und/oder `<port>`, z. B. `https://training.\*/, https://\*.\*`, aber der Platzhalter darf keine Teilzeichenfolge des anzugeben `<hostname>` oder `<port>`.

Das heißt, keine `https://my\*site/` noch `https://\*training\*/` gültig ist. 

Sie können optional überprüfen **einschließen der Unterverzeichnisse und Dateien** auf Übereinstimmung alle Unterverzeichnisse und Dateien, die nach einer URL. Wenn diese Option aktiviert ist und die URL lautet z. B. `https://training`, QoS-Richtlinie berücksichtigt die Anforderungen für` https://training/video` eignet.

#### <a name="to-configure-the-application-name-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Anwendungsname" des Assistenten für QoS-Richtlinie

1. In **diese QoS-Richtlinie gilt für**, wählen Sie entweder **alle Anwendungen** oder **nur Anwendungen mit dieser ausführbaren Datei**.

2. Wenn Sie **Nur Anwendungen, bei denen es sich um folgende ausführbare Datei handelt** auswählen, geben Sie den Namen einer ausführbaren Datei an, der mit der Dateinamenerweiterung EXE endet.

3. Klicken Sie auf **Weiter**.

### <a name="wizard-page-3---ip-addresses"></a>Assistentenseite 3 – IP-Adressen

In der dritten Seite des Assistenten für QoS-Richtlinie können Sie die IP-Adresse-Bedingungen für die QoS-Richtlinie, einschließlich der folgenden angeben:

- Alle Quell- IPv4- oder Quell-IPv6-Adressen oder bestimmte Quell- IPv4- oder Quell-IPv6-Adressen

- Alle Ziel-IPv4- oder IPv6-Adressen oder bestimmte Ziel-IPv4- oder IPv6-Adressen

Wenn Sie **Nur für die folgende Quell-IP-Adresse** oder **Nur für die folgende Ziel-IP-Adresse** auswählen, müssen Sie eines der folgenden Elemente eingeben:

- Ein IPv4-Adresse, z. B. `192.168.1.1`

- IPv4-Adresspräfix mit Netzwerkpräfix-Längenschreibweise, wie `192.168.1.0/24`

- Eine IPv6-Adresse, z. B. `3ffe:ffff::1`

- Eine IPv6-Adresspräfix, z. B. `3ffe:ffff::/48`

Wenn Sie beide auswählen **nur für die folgende Quell-IP-Adresse** und **nur für die folgende Ziel-IP-Adresse**, beide Adressen oder Adresspräfixe muss entweder IPv4 oder IPv6-basierten.

Wenn Sie die URL für HTTP-Server-Anwendungen in der vorherigen Seite des Assistenten angegeben haben, werden Sie feststellen, dass die IP-Quelladresse für die QoS-Richtlinie auf dieser Assistentenseite ausgegraut ist. 

Dies ist "true", da die Quell-IP-Adresse die Adresse des HTTP-Servers ist ein, und es hier nicht konfigurierbar ist. Auf der anderen Seite können Sie die Richtlinie durch Angabe der IP-Zieladresse noch anpassen. Dadurch können Sie verschiedene Richtlinien für verschiedene Clients zu erstellen, indem Sie mit den gleichen HTTP-Server-Anwendungen.

#### <a name="to-configure-the-ip-addresses-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die IP-Adressen-Seite des Assistenten für QoS-Richtlinie

1. In **diese QoS-Richtlinie gilt für** (Quelle), wählen Sie **jede Quelle, IP-Adresse** oder **nur für die folgenden IP-Quelladresse**.

2. Wenn Sie ausgewählt haben **nur die folgenden IP-Quelladresse**, geben Sie eine IPv4- oder IPv6-Adresse oder Präfix.

3. In **diese QoS-Richtlinie gilt für** (Ziel), wählen Sie **jeder Zieladresse** oder **nur für die folgenden IP-Zieladresse.**

4. Wenn Sie ausgewählt haben **nur für die folgenden IP-Zieladresse**, geben Sie eine IPv4- oder IPv6-Adresse oder den Präfix, das den Typ der Adresse entspricht, oder ein Präfix für die Quelladresse angegeben.

5.  Klicken Sie auf **Weiter**.  

### <a name="wizard-page-4---protocols-and-ports"></a>Seite 4 - Protokolle und Ports des Assistenten

Auf der vierten Seite des Assistenten für QoS-Richtlinie können Sie angeben, die Typen des Datenverkehrs und die Ports, die von den Einstellungen auf der ersten Seite des Assistenten gesteuert werden können. Sie können Folgendes angeben:  
-   TCP-Datenverkehr und/oder UDP-Datenverkehr  

-   Alle Quellports, einen Quellportbereich oder einen bestimmten Quellport

-   Alle Zielports, einen Bereich des Zielports oder einen bestimmten Zielport  

#### <a name="to-configure-the-protocols-and-ports-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Protokolle und Ports" des Assistenten für QoS-Richtlinie

1. Wählen Sie unter **Wählen Sie das Protokoll aus, auf das diese QoS-Richtlinie angewendet wird** die Option **TCP**, **UDP** oder **TCP und UDP** aus.

2. Wählen Sie unter **Geben Sie die Quellportnummer an** die Option **Von einem beliebigen Quellport** oder **Von dieser Quellportnummer** aus.

3. Wenn Sie ausgewählt haben **von dieser Quellportnummer**, geben Sie eine Portnummer zwischen 1 und 65535 liegen.

     Optional können Sie einen Portbereich angeben, im Format "*niedrig*:*hohe*,", in denen *mit niedriger* und *hohe* die unteren Grenzen darstellen und obere Grenze des Ports reichen, einschließlich. *Niedrig* und *hohe* jeder muss eine Zahl zwischen 1 und 65535 sein. Zwischen dem Doppelpunkt (:) und den Zahlen ist kein Leerzeichen zulässig.

4. Wählen Sie unter **Geben Sie die Zielportnummer an** die Option **An einen beliebigen Port** oder **An diese Zielportnummer** aus.

5. Wenn Sie im vorherigen Schritt **An diese Zielportnummer** ausgewählt haben, geben Sie eine Portnumber zwischen 1 und 65535 ein.

Um die Erstellung von neuen QoS-Richtlinie abzuschließen, klicken Sie auf **Fertig stellen** auf die **Protokolle und Ports** Seite des Assistenten für QoS-Richtlinie. Abschließend wird die neue QoS-Richtlinie im Detailbereich der Gruppenrichtlinien-Editor aufgeführt.  
  
Zum Anwenden der QoS-Richtlinieneinstellungen auf Benutzer oder Computer verknüpfen Sie das Gruppenrichtlinienobjekt, das in der die QoS-Richtlinien in einer Active Directory Domain Services-Container, z. B. einer Domäne, einer Website oder einer Organisationseinheit (OU) befinden.  
  
##  <a name="bkmk_editpolicy"></a>Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie

Die Seiten des Assistenten beschrieben die QoS-Richtlinie entsprechen zuvor die Eigenschaftenseiten, die angezeigt werden, wenn Sie anzeigen oder bearbeiten Sie die Eigenschaften einer Richtlinie.  
  
### <a name="to-view-the-properties-of-a-qos-policy"></a>So zeigen Sie die Eigenschaften einer QoS-Richtlinie an  
  
-   Mit der rechten Maustaste in den Namen der Richtlinie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **Eigenschaften**.  
  
     Das Gruppenrichtlinienobjekt-Editor zeigt die Eigenschaftenseite mit den folgenden Registerkarten:  
  
    -   "Richtlinienprofil"  
  
    -   Anwendungsname  
  
    -   "IP-Adressen"  
  
    -   Protokolle und Ports  
  
### <a name="to-edit-a-qos-policy"></a>So bearbeiten Sie eine QoS-Richtlinie  
  
-   Mit der rechten Maustaste in den Namen der Richtlinie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **vorhandene Richtlinie bearbeiten**.  
  
     Das Gruppenrichtlinienobjekt-Editor zeigt die **bearbeiten eine vorhandene QoS-Richtlinie** Dialogfeld.  
  
### <a name="to-delete-a-qos-policy"></a>So löschen Sie eine QoS-Richtlinie  
  
-   Mit der rechten Maustaste in den Namen der Richtlinie im Detailbereich der Gruppenrichtlinien-Editor, und klicken Sie dann auf **Richtlinie löschen**.  
  
### <a name="qos-policy-gpmc-reporting"></a>QoS-Richtlinie über Gruppenrichtlinien-Verwaltungskonsole Reporting 

Nachdem Sie eine Reihe von QoS-Richtlinien in Ihrer Organisation angewendet haben, liegt es möglicherweise hilfreich oder notwendig, um in regelmäßigen Abständen zu überprüfen, wie die Richtlinien angewendet werden. Ein Überblick über die QoS-Richtlinien für einen bestimmten Benutzer oder Computer kann mithilfe der Gruppenrichtlinien-Verwaltungskonsole reporting angezeigt werden.  
  
#### <a name="to-run-the-group-policy-results-wizard-for-a-report-of-qos-policies"></a>Zum Ausführen der Gruppenrichtlinienergebnis-Assistenten für einen Bericht von QoS-Richtlinien  
  
-   In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste der **Gruppenrichtlinienergebnisse** Knoten, und wählen Sie im Menü die option zum **Gruppenrichtlinienergebnis-Assistenten.**  
  
Nachdem für Gruppenrichtlinienergebnisse generiert wurden, klicken Sie auf die **Einstellungen** Registerkarte. Auf der **Einstellungen** Registerkarte, die QoS-Richtlinien finden Sie unter den Knoten "Computer Configuration\Windows Settings\QoS Policy" und "User Configuration\Windows Settings\QoS Policy".  
  
Auf der **Einstellungen** Registerkarte, die QoS-Richtlinien sind namentlich QoS-Richtlinie mit ihren DSCP-Wert, der Drosselungsrate, der Bedingungen für Richtlinien und aufgeführt ausschlaggebende Gruppenrichtlinienobjekt in der gleichen Zeile...  
  
Wird das ausschlaggebende Gruppenrichtlinienobjekt wird von der Gruppenrichtlinien-Ergebnisansicht eindeutig identifiziert. Wenn mehrere Gruppenrichtlinienobjekte QoS-Richtlinien, mit dem gleichen Namen der QoS-Richtlinie haben, wird das GPO mit der GPO-Rangfolge angewendet. Dies ist das ausschlaggebende Gruppenrichtlinienobjekt. In Konflikt stehende QoS-Richtlinien (anhand des Namens der Richtlinie gekennzeichnet), die angefügt sind, eine niedrigere Priorität Gruppenrichtlinienobjekt nicht angewendet. Beachten Sie, dass die GPO-Prioritäten definieren die QoS-Richtlinien in der Site, Domäne oder Organisationseinheit, nach Bedarf bereitgestellt werden. Nach der Bereitstellung auf einer Ebene Benutzer oder Computer die [Rangfolgeregeln für QoS-Richtlinie](#BKMK_precedencerules) bestimmen, welcher Datenverkehr zulässig und blockiert ist.  
  
Der QoS-Richtlinie DSCP-Wert, Drosselungsrate und Bedingungen für Richtlinien sind auch in Group Policy Objekt Editor Sperrungsrichtlinie sichtbar  
  
### <a name="advanced-settings-for-roaming-and-remote-users"></a>Erweiterte Einstellungen für roaming und remote Benutzer  
Mit QoS-Richtlinie ist das Ziel, um Datenverkehr über das Netzwerk eines Unternehmens zu verwalten. In mobilen Szenarien können Benutzern Datenverkehr auf oder aus dem Netzwerk des Unternehmens gesendet. Da QoS-Richtlinien nicht von außerhalb des Unternehmens Netzwerk relevant sind, sind die QoS-Richtlinien nur auf Netzwerkschnittstellen aktiviert, die für Windows 8, Windows 7 oder Windows Vista mit dem Unternehmen verbunden sind.  
  
Beispielsweise kann ein Benutzer aus einer kaffeehaus seinen tragbaren Computer mit ihrem Unternehmensnetzwerk über das virtuelle private Netzwerk (VPN) verbinden. Für VPN müssen die physische Netzwerkschnittstelle (z. B. drahtlos) keine QoS-Richtlinien angewendet. Allerdings müssen die VPN-Schnittstelle QoS-Richtlinien angewendet werden, da es für das Unternehmen eine Verbindung herstellt. Wenn der Benutzer später einen anderen Unternehmensnetzwerk, die nicht über eine AD DS-Vertrauensstellung besitzt eingibt, werden die QoS-Richtlinien nicht aktiviert werden.  
  
Beachten Sie, dass diese mobile Szenarien nicht für Server-Workloads gelten. Beispielsweise kann ein Server mit mehreren Netzwerkadaptern auf den Rand Netzwerk eines Unternehmens befinden. Die IT-Abteilung kann auswählen, um QoS-Richtlinien Drosselung des Datenverkehrs zu erhalten, die das Unternehmen egresses; Diese Netzwerkadapter, der diesen ausgehenden Datenverkehr gesendet wird jedoch nicht unbedingt wieder mit dem Unternehmensnetzwerk verbinden. Aus diesem Grund sind die QoS-Richtlinien für alle Netzwerkschnittstellen eines Computers unter Windows Server 2012 immer aktiviert.  
  
> [!NOTE]
>  Selektive Aktivierung gilt nur für QoS-Richtlinien und nicht für die erweiterte QoS-Einstellungen, die in diesem Dokument im nächsten Abschnitt beschrieben.  
  
### <a name="advanced-qos-settings"></a>Erweiterte QoS-Einstellungen

Erweiterte QoS-Einstellungen geben Sie zusätzliche Steuerelemente für IT-Administratoren, um die Auslastung der Computer und DSCP-Markierungen verwalten. Erweiterte QoS-Einstellungen gelten nur auf Computerebene, während die QoS-Richtlinien auf den Computer und die Benutzer angewendet werden können.

#### <a name="to-configure-advanced-qos-settings"></a>So konfigurieren Sie erweiterte QoS-Einstellungen

1.  Klicken Sie auf **Computerkonfiguration**, und klicken Sie dann auf **Windows-Einstellungen in der Gruppenrichtlinie**.
  
2.  Mit der rechten Maustaste **QoS-Richtlinie**, und klicken Sie dann auf **erweiterte QoS-Einstellungen**.

     Die folgende Abbildung zeigt, dass die beiden Registerkarten mit QoS-Einstellungen erweitert: **Eingehende TCP-Datenverkehr** und **DSCP-Markierung Außerkraftsetzung**.
  
> [!NOTE]
>  Erweiterte QoS-Einstellungen sind die gruppenrichtlinieneinstellungen auf Computerebene.
  
#### <a name="advanced-qos-settings-inbound-tcp-traffic"></a>Erweiterte QoS-Einstellungen: eingehende TCP-Datenverkehr

**Eingehende TCP-Datenverkehr** der Auslastung der Netzwerkbandbreite TCP auf der Empfängerseite steuert, während die QoS-Richtlinien für den ausgehenden TCP und UDP-Datenverkehr auswirken. 

Durch Festlegen von einem niedrigeren Durchsatz auf Ebene der **eingehende TCP-Datenverkehr** Registerkarte TCP schränkt die Größe des angekündigten TCP-Empfangsfenster. Die Auswirkung dieser Einstellung wird höhere Durchsatzraten erforderlich sind und -Auslastung für TCP-Verbindungen mit höheren Bandbreiten oder-Wartezeiten (Bandbreite Bandwidth Delay Product) verknüpfen. Standardmäßig werden die Computer unter Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista auf maximalen Durchsatz festgelegt.
  
Das TCP-Empfangsfenster Fenster wurde von früheren Versionen von Windows in Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista geändert. Frühere Versionen von Windows das TCP-Receive-Side-Fenster auf ein Maximum von 64 Kilobyte (KB) eingeschränkt, während es sich bei Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista dynamisch der Receive-Side Fenstergröße bis zu 16 Megabytes (MB ). Im Steuerelement eingehenden TCP-Datenverkehr können Sie die Durchsatzstufe an eingehenden steuern, durch Festlegen den maximalen Wert, den das TCP-Empfangsfenster vergrößert werden kann. Die Ebenen entsprechen die folgenden Höchstwerte. 
  
|Eingehender Durchsatz|Maximal|  
|------------------------|-------|  
|0|64 KB|
|1|256 KB|
|2|1 MB|
|3|16 MB|

Die tatsächliche Fenstergröße kann es sich um einen Wert gleich oder kleiner als die maximal, je nach netzwerkbedingungen sein.

###### <a name="to-set-the-tcp-receive-side-window"></a>Zum Festlegen des TCP-empfangsseitige

1. Im Gruppenrichtlinienobjekt-Editor, klicken Sie auf **lokale Computerrichtlinie**, klicken Sie auf **Windows-Einstellungen**, klicken Sie mit der rechten Maustaste auf **QoS-Richtlinie**, und klicken Sie dann auf **erweiterte QoS- Einstellungen**.
  
2. In **empfangen von TCP-Durchsatz**Option **empfangen von TCP-Durchsatz konfigurieren**, und wählen Sie dann auf der Durchsatzmenge, die Sie möchten.

3.  Verknüpfen Sie das Gruppenrichtlinienobjekt mit der Organisationseinheit.

#### <a name="advanced-qos-settings-dscp-marking-override"></a>Erweiterte QoS-Einstellungen: DSCP-Markierung außer Kraft setzen

Markieren von DSCP außer Kraft setzen, schränkt die Fähigkeit von Anwendungen an, oder "kennzeichnen" – DSCP-Werte, als die in der QoS-Richtlinien. Indem Sie angeben, dass Anwendungen Festlegen von DSCP-Werte zulässig sind, können Anwendungen DSCP-Werten ungleich Null festlegen. 

Durch Angabe **ignorieren**, Anwendungen, die QoS-APIs verwenden, müssen ihre DSCP-Werte, die auf NULL festgelegt, und nur die QoS-Richtlinien können DSCP-Werte festzulegen. 

Standardmäßig zu Computern unter Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista Anwendungen DSCP-Werten an; Anwendungen und Geräte, die nicht die QoS-APIs verwenden, werden nicht überschrieben.

##### <a name="wireless-multimedia-and-dscp-values"></a>Wireless Multimedia und DSCP-Werte

Die [Wi-Fi-Allianz](https://go.microsoft.com/fwlink/?LinkId=160769) hat eine Zertifizierung für Wireless Multimedia eingerichtet \(WMM\) , definiert vier Zugriffskategorien \(WMM_AC\) für die Priorisierung des Netzwerkverkehrs Übertragung über ein WLAN\-Fi-Netzwerk. Die Access-Kategorien enthalten \(in der Reihenfolge der höchsten zum niedrigsten Priorität\): voice, Video, beste Aufwand und Hintergrund; bzw. VO, VI, sein und BK abgekürzt. Die WMM-Spezifikation definiert, welche DSCP Werte entsprechen den vier Kategorien:
  
|DSCP-Wert|Kategorie der WMM-Zugriff|
|----------|-------------------|
|48-63|Sprache (VO)|
|32-47|Video (VI)|
|24-31, 0-7|Beste Leistung (BE)|
|8-23|Hintergrund (s.)|

QoS-Richtlinien, die diese DSCP-Werte zu verwenden, um sicherzustellen, dass diese Portable erstellen, Computer mit dem WLAN\-Fi Certified™ für Drahtlosadapter WMM-Empfangsadapter priorisiert Behandlung, wenn mit WLAN\-Fi für WMM-zertifizierten Punkte zugreifen.
  
### <a name="BKMK_precedencerules"></a>Rangfolgeregeln für QoS-Richtlinie

Ähnlich wie bei der GPO-Prioritäten werden QoS-Richtlinien haben Vorrang vor Regeln zum Lösen von Konflikten, wenn mehrere QoS-Richtlinien auf eine bestimmte Gruppe von Datenverkehr anwenden. Für ausgehende TCP- oder UDP-Datenverkehr kann nur eine QoS-Richtlinie zu einem Zeitpunkt, was bedeutet, dass der QoS-Richtlinien nicht verfügen, dass einen kumulativen Effekt, wie z. B., in denen Drosselung Raten summiert werden würde angewendet werden.

Im Allgemeinen gewinnt die QoS-Richtlinie mit den entsprechenden Bedingungen. Wenn mehrere QoS-Richtlinien anwenden, können die Regeln in drei Kategorien: Benutzerebene im Vergleich zu Computerebene; die Anwendung im Vergleich zu den Netzwerk-Quintupel. und für das Netzwerk quintuple.

Durch *Netzwerk Quintupel*, meinen wir die Quell-IP-Adresse, Ziel-IP-Adresse, Quellport, Zielport und Protokoll \(TCP/UDP\).  

 **QoS-Richtlinie auf Benutzerebene hat Vorrang vor QoS-Richtlinie auf Computerebene**

Mit dieser Regel erleichtert erheblich die Netzwerkadministratoren die Verwaltung von QoS-GPOs, insbesondere für Benutzer-Richtlinien. Z. B. wenn der Netzwerkadministrator eine QoS-Richtlinie für eine Benutzergruppe definieren möchte, können sie einfach erstellen und verteilen ein Gruppenrichtlinienobjekt für diese Gruppe. Sind keine Gedanken machen, zu welchen, denen Computern dieser Benutzer angemeldet sind, und angibt, ob diese Computer müssen in Konflikt stehende QoS-Richtlinien definiert, da, wenn ein Konflikt vorhanden ist, die Richtlinie auf Benutzerebene immer Vorrang hat.

> [!NOTE]
>  Eine QoS-Richtlinie auf Benutzerebene gilt nur für Datenverkehr, der von diesem Benutzer generiert wird. Andere Benutzer von einem bestimmten Computer und den Computer selbst werden keine unterliegen QoS-Richtlinien, die für diesen Benutzer definiert sind.

 **Anwendung Spezifität und Vorrang vor den über das Netzwerk Quintupel**

Wenn mehrere QoS-Richtlinien für den Datenverkehr eines bestimmten übereinstimmen, wird die spezifische Richtlinie angewendet. Zwischen Richtlinien, die Anwendungen zu identifizieren, eine Richtlinie, die sendende Anwendung Dateipfad enthält, spezifischer als eine andere Richtlinie gilt, die nur den Anwendungsnamen (kein Pfad) identifiziert. Wenn mehrere Richtlinien mit Anwendungen trotzdem anwenden möchten, verwenden die Rangfolgeregeln des Netzwerks Quintupel die beste Übereinstimmung gefunden.

Alternativ können mehrere QoS-Richtlinien auf den gleichen Datenverkehr durch Angeben von Bedingungen mit nicht überlappenden anwenden. Zwischen den Bedingungen der Anwendungen und das Netzwerk Quintupel die Richtlinie, die angibt, die Anwendung wird als spezifischer und wird angewendet. 

Z. B. Policy_A gibt nur einen Anwendungsnamen (app.exe), und Policy_B gibt an, die Ziel-IP-Adresse 192.168.1.0/24. Wenn diese QoS-Richtlinien in Konflikt stehen \(app.exe sendet Datenverkehr an eine IP-Adresse innerhalb des Bereichs von 192.168.4.0/24\), Policy_A angewendet.

 **Erhöhung der Genauigkeit hat Vorrang vor innerhalb des Netzwerks Quintupel**

Bei Richtlinienkonflikten in der Netzwerk-Quintupel hat die Richtlinie mit den meisten übereinstimmenden Bedingungen Vorrang vor. Nehmen wir beispielsweise an, dass Policy_C gibt an, Quell-IP-Adresse "Beliebig", Ziel-IP-Adresse 10.0.0.1, Quelle "any", port, Ziel "any" port und Protokoll "TCP". 

Als Nächstes wird davon ausgegangen Sie, dass Policy_D gibt an, Quell-IP-Adresse "any", Ziel-IP-Adresse 10.0.0.1, Quellport "Beliebig", Ziel-Port 80 und Protokoll "TCP". Klicken Sie dann mit Policy_C und Policy_D Verbindungen mit dem Ziel 10.0.0.1:80 übereinstimmen. Da die QoS-Richtlinie auf die Richtlinie mit den spezifischsten übereinstimmenden Bedingungen gilt, Vorrang Policy_D in diesem Beispiel.  
  
Jedoch möglicherweise die QoS-Richtlinien eine gleiche Anzahl von Bedingungen. Z. B. mehrere Richtlinien können jede Geben Sie nur eine (aber nicht identisch) Teil der Netzwerk-Quintupel. Ist der folgende Reihenfolge zwischen den Quintupel Netzwerk von hoch zu niedrig Vorrang vor:

- Quell-IP-Adresse

- Ziel-IP-Adresse

- Quellport

- Zielport

- Protokoll (TCP oder UDP)

Innerhalb einer bestimmten Bedingung, z. B. IP-Adresse wird eine spezifische IP-Adresse mit höherer Priorität behandelt. Beispielsweise ist eine IP-Adresse 192.168.4.1 spezifischer als 192.168.4.0/24.

Entwerfen Sie Ihre QoS-Richtlinien so genau wie möglich zur Vereinfachung Ihrer Organisation die Möglichkeit, zu verstehen, welche Richtlinien wirksam sind.

Im nächsten Thema in diesem Handbuch finden Sie unter [QoS-Richtlinie-Ereignisse und-Fehler](qos-policy-errors.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
