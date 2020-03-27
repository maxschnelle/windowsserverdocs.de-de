---
title: Verwalten der QoS-Richtlinie
description: Dieses Thema enthält Anweisungen zum Erstellen und Verwalten von Quality of Service-Richtlinien (QoS) in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 04fdfa54-6600-43d4-8945-35f75e15275a
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36c30372b6cac40b603658eca9636a265801fb1a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315442"
---
# <a name="manage-qos-policy"></a>Verwalten der QoS-Richtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie den QoS-Richtlinien-Assistenten zum Erstellen, bearbeiten oder Löschen einer QoS-Richtlinie verwenden.

>[!NOTE]
>  Zusätzlich zu diesem Thema ist die folgende Dokumentation zur QoS-Richtlinien Verwaltung verfügbar.
> 
>  - [Ereignisse und Fehler in der QoS-Richtlinie](qos-policy-errors.md)

In Windows-Betriebssystemen kombiniert die QoS-Richtlinie die Funktionalität der Standard basierten QoS mit der Verwaltbarkeit von Gruppenrichtlinie. Diese Kombination ermöglicht die einfache Anwendung von QoS-Richtlinien zum Gruppenrichtlinie von Objekten. Windows enthält einen QoS-Richtlinien-Assistenten, der Sie beim Ausführen der folgenden Aufgaben unterstützt.

-  [Erstellen einer QoS-Richtlinie](#bkmk_createpolicy)

-  [Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie](#bkmk_editpolicy)

##  <a name="create-a-qos-policy"></a><a name="bkmk_createpolicy"></a>Erstellen einer QoS-Richtlinie

Bevor Sie eine QoS-Richtlinie erstellen, ist es wichtig, dass Sie die beiden Schlüssel-QoS-Steuerelemente kennen, die zur Verwaltung des Netzwerk Datenverkehrs verwendet werden:

- DSCP-Wert

-   Drosselungs Rate

### <a name="prioritizing-traffic-with-dscp"></a>Priorisieren von Datenverkehr mit DSCP

Wie bereits im vorherigen Beispiel für eine Branchen Anwendung erwähnt, können Sie die Priorität des ausgehenden Netzwerk Datenverkehrs definieren. verwenden Sie hierzu **DSCP-Wert angeben** , um eine QoS-Richtlinie mit einem bestimmten DSCP-Wert zu konfigurieren. 

Wie in RFC 2474 beschrieben, ermöglicht DSCP das Angeben von Werten zwischen 0 und 63 im Feld "TOS" eines IPv4-Pakets und innerhalb des Felds "Traffic Class" in IPv6. Netzwerk Router verwenden den DSCP-Wert, um Netzwerkpakete zu klassifizieren und entsprechend in die Warteschlange zu stellen.
  
> [!NOTE]
>  Standardmäßig weist Windows-Datenverkehr den DSCP-Wert 0 auf.
  
Die Anzahl der Warteschlangen und deren Priorisierungsverhalten muss im Rahmen der QoS-Strategie der Organisation festgelegt werden. Ihre Organisation kann z. b. über fünf Warteschlangen verfügen: Latenz bezogener Datenverkehr, Steuerungs Datenverkehr, geschäftskritischer Datenverkehr, bestmöglicher Datenverkehr und Massen Datenübertragung.  
  
### <a name="throttling-traffic"></a>Drosseln des Datenverkehrs

Neben DSCP-Werten ist die Drosselung eine weitere wichtige Kontrolle für die Verwaltung der Netzwerkbandbreite. Wie bereits erwähnt, können Sie die Einstellung **Drosselungs Rate angeben** verwenden, um eine QoS-Richtlinie mit einer bestimmten Drosselungs Rate für ausgehenden Datenverkehr zu konfigurieren. Mithilfe der Drosselung schränkt eine QoS-Richtlinie den ausgehenden Netzwerk Datenverkehr auf eine angegebene Drosselungs Rate ein. DSCP-Markierung und Drosselung können gemeinsam verwendet werden, um den Datenverkehr effektiv zu verwalten.

>[!NOTE]
>Das Kontrollkästchen **Drosselungsrate angeben** ist standardmäßig nicht aktiviert.

Wenn Sie eine QoS-Richtlinie erstellen möchten, bearbeiten Sie die Einstellungen eines Gruppenrichtlinie Objekts (GPO) im Gruppenrichtlinien-Verwaltungskonsole (GPMC)-Tool. Die GPMC öffnet dann die Gruppenrichtlinienobjekt-Editor.

QoS-Richtliniennamen müssen eindeutig sein. Wie Richtlinien auf Server und Endbenutzer angewendet werden, hängt davon ab, wo die QoS-Richtlinie im Gruppenrichtlinienobjekt-Editor gespeichert ist:

- Eine QoS-Richtlinie in Computerkonfiguration\Windows-einstellungen\qos-Richtlinie gilt für Computer, unabhängig vom aktuell angemeldeten Benutzer. Normalerweise verwenden Sie computerbasierte QoS-Richtlinien für Servercomputer.

- Eine QoS-Richtlinie in Benutzerkonfiguration\Windows-einstellungen\qos-Richtlinie gilt für Benutzer, nachdem Sie sich angemeldet haben, unabhängig davon, bei welchem Computer Sie angemeldet sind.

#### <a name="to-create-a-new-qos-policy-with-the-qos-policy-wizard"></a>So erstellen Sie eine neue QoS-Richtlinie mit dem QoS-Richtlinien-Assistenten

-   Klicken Sie in Gruppenrichtlinienobjekt-Editor mit der rechten Maustaste auf einen der Knoten der **QoS-Richtlinie** , und klicken Sie dann auf **neue Richtlinie erstellen**.

### <a name="wizard-page-1---policy-profile"></a>Seite 1 des Assistenten: Richtlinien Profil

Auf der ersten Seite des Assistenten für QoS-Richtlinien können Sie einen Richtlinien Namen angeben und konfigurieren, wie QoS ausgehenden Netzwerk Datenverkehr steuert.

#### <a name="to-configure-the-policy-profile-page-of-the-qos-based-policy-wizard"></a>So konfigurieren Sie die Seite "Richtlinienprofil" des Assistenten für richtlinienbasierten QoS

1. Geben Sie in das Feld **Richtlinienname** einen Namen für die QoS-Richtlinie ein. Der Name muss die Richtlinie eindeutig identifizieren.

2. Verwenden Sie optional **DSCP-Wert angeben** , um die DSCP-Markierung zu aktivieren, und konfigurieren Sie dann einen DSCP-Wert zwischen 0 und 63.

3. Verwenden Sie optional **Drosselungsrate angeben**, um die Datenverkehrsdrosselung zu aktivieren und die Drosselungsrate zu konfigurieren. Der Wert für die Drosselungs Rate muss größer als 1 sein, und Sie können Einheiten von Kilobyte pro Sekunde \(Kbit/s\) oder Megabyte pro Sekunde \(Mbit/s\)angeben.

4. Klicken Sie auf **Weiter**.

### <a name="wizard-page-2---application-name"></a>Assistenten Seite 2: Anwendungs Name

Auf der zweiten Seite des Assistenten für QoS-Richtlinien können Sie die Richtlinie auf alle Anwendungen anwenden, auf eine bestimmte Anwendung, die durch den Namen der ausführbaren Datei, einen Pfad und einen Anwendungsnamen identifiziert wird, oder auf die HTTP-Server Anwendungen, die Anforderungen für eine bestimmte URL verarbeiten.

- **Alle Anwendungen** gibt an, dass die Einstellungen für die Datenverkehrs Verwaltung auf der ersten Seite des Assistenten für QoS-Richtlinien auf alle Anwendungen angewendet werden.

- **Nur Anwendungen mit diesem Namen der ausführbaren Datei** geben an, dass die Einstellungen für die Datenverkehrs Verwaltung auf der ersten Seite des QoS-Richtlinien Assistenten für eine bestimmte Anwendung gelten. Der Name der ausführbaren Datei muss die Dateinamenerweiterung EXE aufweisen.

- **Nur HTTP-Server Anwendungen, die auf Anforderungen für diese URL reagieren** , geben an, dass die Einstellungen für die Datenverkehrs Verwaltung auf der ersten Seite des QoS-Richtlinien Assistenten nur für bestimmte HTTP-Server Anwendungen gelten.

Optional können Sie den Anwendungspfad eingeben. Zum Angeben des Anwendungspfads geben Sie den Pfad zusammen mit dem Anwendungsnamen ein. Der Pfad kann Umgebungsvariablen enthalten. Beispiele: "%ProgramFiles%\Mein Anwendungspfad\MeineAnwendung.exe" oder "C:\Programme\Mein Anwendungspfad\MeineAnwendung.exe".

>[!NOTE]
>Der Anwendungspfad darf keinen Pfad enthalten, der zu einer symbolischen Verknüpfung aufgelöst wird.

Die URL muss in Form von `http[s]://<hostname\>:<port\>/<url-path>`[RFC 1738](https://tools.ietf.org/html/rfc1738)entsprechen. Sie können einen Platzhalter, `‘*'`für `<hostname>` und/oder `<port>`verwenden, z. b. `https://training.\*/, https://\*.\*`, aber der Platzhalter darf keine Teil Zeichenfolge `<hostname>` oder `<port>`bezeichnen.

Anders ausgedrückt: weder `https://my\*site/` noch `https://\*training\*/` ist gültig. 

Optional können Sie **Unterverzeichnisse und Dateien einschließen** aktivieren, um den Abgleich für alle Unterverzeichnisse und Dateien nach einer URL auszuführen. Wenn diese Option z. b. aktiviert ist und die URL `https://training`ist, werden Anforderungen von der QoS-Richtlinie` https://training/video` eine gute Entsprechung berücksichtigt.

#### <a name="to-configure-the-application-name-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Anwendungs Name" des Assistenten für QoS-Richtlinien

1. Wählen Sie unter **Diese QoS-Richtlinie gilt für**entweder **alle Anwendungen** oder **nur Anwendungen mit diesem Namen der ausführbaren Datei**aus.

2. Wenn Sie **Nur Anwendungen, bei denen es sich um folgende ausführbare Datei handelt** auswählen, geben Sie den Namen einer ausführbaren Datei an, der mit der Dateinamenerweiterung EXE endet.

3. Klicken Sie auf **Weiter**.

### <a name="wizard-page-3---ip-addresses"></a>Assistenten Seite 3-IP-Adressen

Auf der dritten Seite des Assistenten für QoS-Richtlinien können Sie IP-Adress Bedingungen für die QoS-Richtlinie angeben, einschließlich der folgenden:

- Alle Quell- IPv4- oder Quell-IPv6-Adressen oder bestimmte Quell- IPv4- oder Quell-IPv6-Adressen

- Alle IPv4-oder IPv6-Zieladressen oder bestimmte IPv4-oder IPv6-Zieladressen

Wenn Sie **Nur für die folgende Quell-IP-Adresse** oder **Nur für die folgende Ziel-IP-Adresse** auswählen, müssen Sie eines der folgenden Elemente eingeben:

- Eine IPv4-Adresse, z. b. `192.168.1.1`

- Ein IPv4-Adress Präfix mit Netzwerk Präfix-Längen Notation, z. b. `192.168.1.0/24`

- Eine IPv6-Adresse, z. b. `3ffe:ffff::1`

- Ein IPv6-Adress Präfix, z. b. `3ffe:ffff::/48`

Wenn Sie **nur für die folgende Quell-IP-Adresse** und **nur für die folgende Ziel-IP-Adresse**auswählen, müssen beide Adressen oder Adress Präfixe entweder IPv4-oder IPv6-basiert sein.

Wenn Sie auf der vorherigen Seite des Assistenten die URL für http-Server Anwendungen angegeben haben, werden Sie feststellen, dass die IP-Quelladresse für die QoS-Richtlinie auf dieser Seite des Assistenten ausgegraut ist. 

Dies trifft zu, weil die IP-Quelladresse die HTTP-Server Adresse ist und hier nicht konfiguriert werden kann. Andererseits können Sie die Richtlinie dennoch anpassen, indem Sie die Ziel-IP-Adresse angeben. Dies ermöglicht es Ihnen, unterschiedliche Richtlinien für verschiedene Clients mit denselben http-Server Anwendungen zu erstellen.

#### <a name="to-configure-the-ip-addresses-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "IP-Adressen" des Assistenten für QoS-Richtlinien

1. Wählen Sie unter **Diese QoS-Richtlinie gilt** für (Quelle) die Option **beliebige Quell-IP-Adresse** oder **nur für die folgende IP-Quelladresse aus**.

2. Wenn Sie **nur die folgende IP-Quelladresse**ausgewählt haben, geben Sie eine IPv4-oder IPv6-Adresse oder ein Präfix an.

3. Wählen Sie unter **Diese QoS-Richtlinie gilt** für (Ziel) die Option **beliebige Zieladresse** oder **nur für die folgende IP-Zieladresse aus.**

4. Wenn Sie **nur für die folgende IP-Zieladresse**ausgewählt haben, geben Sie eine IPv4-oder IPv6-Adresse oder ein Präfix an, die dem Typ der Adresse oder des Präfixes entspricht, das für die Quelladresse angegeben

5.  Klicken Sie auf **Weiter**.  

### <a name="wizard-page-4---protocols-and-ports"></a>Assistenten Seite 4: Protokolle und Ports

Auf der vierten Seite des Assistenten für QoS-Richtlinien können Sie die Arten des Datenverkehrs und die Ports angeben, die über die Einstellungen auf der ersten Seite des Assistenten gesteuert werden. Sie können Folgendes angeben:  
-   TCP-Datenverkehr und/oder UDP-Datenverkehr  

-   Alle Quellports, einen Quellportbereich oder einen bestimmten Quellport

-   Alle Zielports, eine Reihe von Zielports oder ein bestimmter Zielport  

#### <a name="to-configure-the-protocols-and-ports-page-of-the-qos-policy-wizard"></a>So konfigurieren Sie die Seite "Protokolle und Ports" des Assistenten für QoS-Richtlinien

1. Wählen Sie unter **Wählen Sie das Protokoll aus, auf das diese QoS-Richtlinie angewendet wird** die Option **TCP**, **UDP** oder **TCP und UDP** aus.

2. Wählen Sie unter **Geben Sie die Quellportnummer an** die Option **Von einem beliebigen Quellport** oder **Von dieser Quellportnummer** aus.

3. Wenn Sie **von dieser Quell Portnummer**ausgewählt haben, geben Sie eine Portnummer zwischen 1 und 65535 ein.

     Optional können Sie einen Port Bereich im Format "*Low*:*High*" angeben, wobei " *Low* " und " *High* " die unteren und oberen Begrenzungen des Port Bereichs einschließen. " *Niedrig* " und " *hoch* " müssen eine Zahl zwischen 1 und 65535 sein. Zwischen dem Doppelpunkt (:) und den Zahlen ist kein Leerzeichen zulässig.

4. Wählen Sie unter **Geben Sie die Zielportnummer an** die Option **An einen beliebigen Port** oder **An diese Zielportnummer** aus.

5. Wenn Sie im vorherigen Schritt **An diese Zielportnummer** ausgewählt haben, geben Sie eine Portnumber zwischen 1 und 65535 ein.

Um die Erstellung der neuen QoS-Richtlinie abzuschließen, klicken Sie auf der Seite **Protokolle und Ports** des QoS-Richtlinien-Assistenten auf **Fertig** stellen. Nach Abschluss des Vorgangs wird die neue QoS-Richtlinie im Detailbereich der Gruppenrichtlinienobjekt-Editor aufgeführt.  
  
Wenn Sie die QoS-Richtlinien Einstellungen auf Benutzer oder Computer anwenden möchten, verknüpfen Sie das Gruppenrichtlinien Objekt, in dem sich die QoS-Richtlinien befinden, mit einem Active Directory Domain Services Container (z. b. einer Domäne, einem Standort oder einer Organisationseinheit).  
  
##  <a name="view-edit-or-delete-a-qos-policy"></a><a name="bkmk_editpolicy"></a>Anzeigen, bearbeiten oder Löschen einer QoS-Richtlinie

Die Seiten des zuvor beschriebenen Assistenten für QoS-Richtlinien entsprechen den Eigenschaften Seiten, die angezeigt werden, wenn Sie die Eigenschaften einer Richtlinie anzeigen oder bearbeiten.  
  
### <a name="to-view-the-properties-of-a-qos-policy"></a>So zeigen Sie die Eigenschaften einer QoS-Richtlinie an  
  
-   Klicken Sie im Detailbereich der Gruppenrichtlinienobjekt-Editor mit der rechten Maustaste auf den Richtlinien Namen, und klicken Sie dann auf **Eigenschaften**.  
  
     Die Gruppenrichtlinienobjekt-Editor zeigt die Eigenschaften Seite mit den folgenden Registerkarten an:  
  
    -   "Richtlinienprofil"  
  
    -   Anwendungsname  
  
    -   IP-Adressen  
  
    -   Protokolle und Ports  
  
### <a name="to-edit-a-qos-policy"></a>So bearbeiten Sie eine QoS-Richtlinie  
  
-   Klicken Sie im Detailbereich der Gruppenrichtlinienobjekt-Editor mit der rechten Maustaste auf den Richtlinien Namen, und klicken Sie dann auf **vorhandene Richtlinie bearbeiten**.  
  
     Die Gruppenrichtlinienobjekt-Editor zeigt das Dialogfeld **vorhandene QoS-Richtlinie bearbeiten an** .  
  
### <a name="to-delete-a-qos-policy"></a>So löschen Sie eine QoS-Richtlinie  
  
-   Klicken Sie im Detailbereich der Gruppenrichtlinienobjekt-Editor mit der rechten Maustaste auf den Richtlinien Namen, und klicken Sie dann auf **Richtlinie löschen**.  
  
### <a name="qos-policy-gpmc-reporting"></a>Berichterstellung der QoS-Richtlinie GPMC 

Nachdem Sie eine Reihe von QoS-Richtlinien in Ihrer Organisation angewendet haben, ist es möglicherweise hilfreich oder notwendig, regelmäßig zu überprüfen, wie die Richtlinien angewendet werden. Eine Zusammenfassung der QoS-Richtlinien für einen bestimmten Benutzer oder Computer kann mithilfe der GPMC-Berichterstattung angezeigt werden.  
  
#### <a name="to-run-the-group-policy-results-wizard-for-a-report-of-qos-policies"></a>So führen Sie den Assistenten für Gruppenrichtlinie Ergebnisse für einen Bericht der QoS-Richtlinien aus  
  
-   Klicken Sie in GPMC mit der rechten Maustaste auf den Knoten **Gruppenrichtlinie Ergebnisse** , und wählen Sie dann die Menüoption für **Gruppenrichtlinie Ergebnis-Assistenten aus.**  
  
Nachdem Gruppenrichtlinie Ergebnisse generiert wurden, klicken Sie auf die Registerkarte **Einstellungen** . Auf der Registerkarte **Einstellungen** befinden sich die QoS-Richtlinien unter "Computerkonfiguration\Windows-einstellungen\qos-Richtlinie" und "Benutzerkonfiguration\Windows-einstellungen\qos-Richtlinie"  
  
Auf der Registerkarte **Einstellungen** werden die QoS-Richtlinien nach Ihren QoS-Richtlinien Namen mit Ihrem DSCP-Wert, der Drosselungs Rate, den Richtlinien Bedingungen und dem gewinnenden GPO in derselben Zeile aufgelistet.  
  
Die Gruppenrichtlinie Ergebnis Ansicht identifiziert das gewinnende Gruppenrichtlinien Objekt eindeutig. Wenn mehrere Gruppenrichtlinien Objekte über QoS-Richtlinien mit demselben QoS-Richtlinien Namen verfügen, wird das Gruppenrichtlinien Objekt mit der höchsten Rangfolge für das Gruppenrichtlinien Objekt angewendet. Dies ist das gewinnende Gruppenrichtlinien Objekt. In Konflikt stehende QoS-Richtlinien (identifiziert durch Richtlinien Name), die an ein GPO mit niedrigerer Priorität angefügt sind, werden nicht angewendet. Beachten Sie, dass die GPO-Prioritäten definieren, welche QoS-Richtlinien je nach Bedarf in der Site, Domäne oder Organisationseinheit bereitgestellt werden. Nach der Bereitstellung auf Benutzer-oder Computer Ebene bestimmen die [Rangfolge der QoS-Richtlinien](#BKMK_precedencerules) , welcher Datenverkehr zugelassen und blockiert wird.  
  
Der DSCP-Wert, die Drosselungs Rate und die Richtlinien Bedingungen der QoS-Richtlinie sind auch in Gruppenrichtlinienobjekt-Editor (GPOE) sichtbar.  
  
### <a name="advanced-settings-for-roaming-and-remote-users"></a>Erweiterte Einstellungen für Roaming und Remote Benutzer  
Mit der QoS-Richtlinie besteht das Ziel darin, den Datenverkehr im Netzwerk eines Unternehmens zu verwalten. In mobilen Szenarios senden Benutzer möglicherweise Datenverkehr an das Unternehmensnetzwerk. Da QoS-Richtlinien nicht von dem Netzwerk des Unternehmens abhängen, sind QoS-Richtlinien nur auf Netzwerkschnittstellen aktiviert, die für Windows 8, Windows 7 oder Windows Vista mit dem Unternehmen verbunden sind.  
  
Beispielsweise kann ein Benutzer ihren tragbaren Computer über ein virtuelles privates Netzwerk (VPN) über ein Kaffeegeschäft mit dem Netzwerk Ihres Unternehmens verbinden. Für VPN werden für die physische Netzwerkschnittstelle (z. b. drahtlos) keine QoS-Richtlinien angewendet. Für die VPN-Schnittstelle werden jedoch QoS-Richtlinien angewendet, da Sie mit dem Unternehmen verbunden ist. Wenn der Benutzer zu einem späteren Zeitpunkt ein anderes Netzwerk eines Unternehmens eingibt, das nicht über eine AD DS Vertrauensstellung verfügt, werden keine QoS-Richtlinien aktiviert.  
  
Beachten Sie, dass diese mobilen Szenarien nicht für Server Arbeits Auslastungen gelten. Beispielsweise kann sich ein Server mit mehreren Netzwerkadaptern am Rand des Netzwerks eines Unternehmens befinden. Die IT-Abteilung könnte festlegen, dass QoS-Richtlinien den Datenverkehr Drosseln, der das Unternehmen auswählt. der Netzwerkadapter, der diesen ausgehenden Datenverkehr sendet, stellt jedoch nicht notwendigerweise eine Verbindung mit dem Unternehmensnetzwerk her. Aus diesem Grund sind QoS-Richtlinien auf allen Netzwerkschnittstellen eines Computers, auf dem Windows Server 2012 ausgeführt wird, immer aktiviert.  
  
> [!NOTE]
>  Selektive Aktivierung gilt nur für QoS-Richtlinien und nicht für die erweiterten QoS-Einstellungen, die weiter unten in diesem Dokument erläutert werden.  
  
### <a name="advanced-qos-settings"></a>Erweiterte QoS-Einstellungen

Erweiterte QoS-Einstellungen bieten IT-Administratoren zusätzliche Steuerungsmechanismen für die Verwaltung von Computernetzwerk Verbrauch und DSCP-Kennzeichnungen. Erweiterte QoS-Einstellungen gelten nur auf Computer Ebene, während QoS-Richtlinien auf der Computer-und der Benutzerebene angewendet werden können.

#### <a name="to-configure-advanced-qos-settings"></a>So konfigurieren Sie erweiterte QoS-Einstellungen

1.  Klicken Sie auf **Computer Konfiguration**, und klicken Sie dann **in Gruppenrichtlinie auf Windows-Einstellungen**.
  
2.  Klicken Sie mit der rechten Maustaste auf **QoS Policy**, und klicken Sie dann auf **Erweiterte QoS-Einstellungen**.

     In der folgenden Abbildung werden die beiden erweiterten Registerkarten für die QoS-Einstellungen gezeigt: **eingehender TCP-Datenverkehr** und **außer Kraft**setzung der d
  
> [!NOTE]
>  Erweiterte QoS-Einstellungen sind Gruppenrichtlinie Einstellungen auf Computer Ebene.
  
#### <a name="advanced-qos-settings-inbound-tcp-traffic"></a>Erweiterte QoS-Einstellungen: eingehender TCP-Datenverkehr

**Eingehender TCP-Datenverkehr** steuert den TCP-Bandbreitenverbrauch auf Empfängerseite, während QoS-Richtlinien den ausgehenden TCP-und UDP-Datenverkehr beeinflussen. 

Durch Festlegen einer niedrigeren Durchsatz Ebene auf der Registerkarte **eingehender TCP-Datenverkehr** beschränkt TCP die Größe des angekündigten TCP-Empfangs Fensters. Diese Einstellung wirkt sich auf höhere Durchsatzraten und die Verbindungs Auslastung für TCP-Verbindungen mit höheren Bandbreiten oder Latenzen (Bandbreiten Verzögerung) aus. Standardmäßig sind Computer, auf denen Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista ausgeführt wird, auf den maximalen Durchsatz festgelegt.
  
Das TCP-Empfangs Fenster wurde in Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista aus früheren Windows-Versionen geändert. In früheren Versionen von Windows wurde das Empfangs seitige TCP-Fenster auf maximal 64 Kilobyte (KB) beschränkt, während Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista die Größe des Empfangs seitigen Fensters dynamisch auf bis zu 16 Megabyte (MB ). In der eingehenden TCP-Datenverkehrs Steuerung können Sie den Durchsatz für den eingehenden Durchsatz steuern, indem Sie den maximalen Wert festlegen, auf den das TCP-Empfangs Fenster vergrößert werden kann. Die Ebenen entsprechen den folgenden maximalen Werten. 
  
|Durchsatz für eingehenden Durchsatz|Maximum|  
|------------------------|-------|  
|0|64 KB|
|1|256 KB|
|2|1 MB|
|3|16 MB|

Die tatsächliche Fenstergröße kann je nach Netzwerkbedingungen ein Wert sein, der größer oder kleiner als der Höchstwert ist.

###### <a name="to-set-the-tcp-receive-side-window"></a>Festlegen des TCP-Empfangs seitigen Fensters

1. Klicken Sie in Gruppenrichtlinienobjekt-Editor auf **Richtlinie für den lokalen Computer**, klicken Sie auf **Windows-Einstellungen**, klicken Sie mit der rechten Maustaste auf **QoS-Richtlinie**, **und klicken Sie**
  
2. Wählen Sie unter **TCP-Empfangs Durchsatz**die Option **TCP-Empfangs Durchsatz konfigurieren**aus, und wählen Sie dann die gewünschte Durchsatz Ebene aus.

3.  Verknüpfen Sie das GPO mit der Organisationseinheit.

#### <a name="advanced-qos-settings-dscp-marking-override"></a>Erweiterte QoS-Einstellungen: außer Kraft setzung der DSCP-Markierung

Die Überschreibung der DSCP-Markierung schränkt die Fähigkeit von Anwendungen ein, –-oder "Mark"-–-DSCP-Werte anzugeben, die in QoS-Richtlinien angegeben sind Wenn Sie angeben, dass Anwendungen DSCP-Werte festlegen dürfen, können Anwendungen nicht-NULL-DSCP-Werte festlegen. 

Durch die Angabe von **Ignore**werden die DSCP-Werte für Anwendungen, die QoS-APIs verwenden, auf NULL festgelegt, und nur QoS-Richtlinien können DSCP-Werte festlegen. 

Standardmäßig ermöglichen Computer mit Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista die Angabe von DSCP-Werten. Anwendungen und Geräte, die nicht die QoS-APIs verwenden, werden nicht überschrieben.

##### <a name="wireless-multimedia-and-dscp-values"></a>Drahtlose Multimedia-und DSCP-Werte

Die [Wi-Fi-Allianz](https://go.microsoft.com/fwlink/?LinkId=160769) hat eine Zertifizierung für drahtlose Multimedia-\(WMM-\) eingerichtet, die vier Zugriffs Kategorien definiert \(WMM_AC\) zum Priorisieren von Netzwerk Datenverkehr, der in einem Drahtlos Netzwerk mit Wi-\-fi übertragen wird. Die Zugriffs Kategorien enthalten \(in der Reihenfolge, in der die höchste Priorität\)ist: sprach-, Video-, Best-und Hintergrundinformationen. jeweils als VO, VI, be und BK abgekürzt. Die WMM-Spezifikation definiert, welche DSCP-Werte mit den vier Zugriffs Kategorien übereinstimmen:
  
|DSCP-Wert|WMM-Zugriffs Kategorie|
|----------|-------------------|
|48-63|Stimme (VO)|
|32-47|Video (VI)|
|24-31, 0-7|Bewährter Aufwand (ist)|
|8-23|Hintergrund (BK)|

Sie können QoS-Richtlinien erstellen, die diese DSCP-Werte verwenden, um sicherzustellen, dass tragbare Computer mit Wi\-Fi-zertifizierten™ für WMM-drahtlos Adapter eine priorisierte Behandlung erhalten, wenn Sie für WMM-Zugriffspunkte mit\-WLAN-Zertifizierung verknüpft sind.
  
### <a name="qos-policy-precedence-rules"></a><a name="BKMK_precedencerules"></a>Rangfolge von QoS-Richtlinien

Ähnlich wie bei den Prioritäten von GPO haben QoS-Richtlinien Vorrangregeln zum Auflösen von Konflikten, wenn mehrere QoS-Richtlinien für eine bestimmte Gruppe von Datenverkehr gelten. Für ausgehenden TCP-oder UDP-Datenverkehr kann jeweils nur eine QoS-Richtlinie angewendet werden. Dies bedeutet, dass QoS-Richtlinien keinen kumulativen Effekt haben, z. b. wenn Drosselungs Raten summiert werden.

Im allgemeinen gewinnt die QoS-Richtlinie mit den meisten übereinstimmenden Bedingungen. Wenn mehrere QoS-Richtlinien angewendet werden, können die Regeln in drei Kategorien unterteilt werden: auf Benutzerebene und auf Computer Ebene. Anwendung im Vergleich zum Netzwerk-quintupel; und unter dem Netzwerk-quintupel.

Der *Netzwerk-quintupel*bedeutet, dass die Quell-IP-Adresse, Ziel-IP-Adresse, Quellport, Zielport und Protokoll \(TCP/UDP\).  

 **Die QoS-Richtlinie auf Benutzerebene hat Vorrang vor der QoS-Richtlinie auf Computer Ebene.**

Diese Regel vereinfacht die Verwaltung von QoS-GPOs durch Netzwerkadministratoren, insbesondere für Richtlinien auf Grundlage von Benutzergruppen –. Wenn der Netzwerkadministrator beispielsweise eine QoS-Richtlinie für eine Benutzergruppe definieren möchte, kann er nur ein Gruppenrichtlinien Objekt erstellen und an diese Gruppe verteilen. Sie müssen sich keine Gedanken darüber machen, bei welchen Computern diese Benutzer angemeldet sind und ob für diese Computer widersprüchliche QoS-Richtlinien definiert sind, denn wenn ein Konflikt vorliegt, hat die Richtlinie auf Benutzerebene immer Vorrang.

> [!NOTE]
>  Eine QoS-Richtlinie auf Benutzerebene gilt nur für Datenverkehr, der von diesem Benutzer generiert wird. Andere Benutzer eines bestimmten Computers und der Computer selbst unterliegen keinen QoS-Richtlinien, die für diesen Benutzer definiert sind.

 **Anwendungs Spezifizität und Vorrang vor Netzwerk-quintupel**

Wenn mehrere QoS-Richtlinien mit dem spezifischen Datenverkehr identisch sind, wird die spezifischere Richtlinie angewendet. In Richtlinien, mit denen Anwendungen identifiziert werden, wird eine Richtlinie, die den Dateipfad der Sende Anwendung einschließt, als genauer betrachtet als eine andere Richtlinie, die nur den Anwendungsnamen identifiziert (kein Pfad). Wenn mehrere Richtlinien mit Anwendungen weiterhin zutreffen, verwenden die Rang Folge Regeln das netzwerkquintupel, um die beste Entsprechung zu finden.

Sie können auch mehrere QoS-Richtlinien auf denselben Datenverkehr anwenden, indem Sie nicht überlappende Bedingungen angeben. Zwischen den Bedingungen von Anwendungen und dem Netzwerk-quintupel wird die Richtlinie, die die Anwendung angibt, als spezifischere angesehen und angewendet. 

Beispielsweise gibt policy_A nur einen Anwendungsnamen (app. exe) an, und policy_B gibt die Ziel-IP-Adresse 192.168.1.0/24 an. Wenn diese QoS-Richtlinien in Konflikt stehen \(app. exe Datenverkehr an eine IP-Adresse im Bereich von 192.168.4.0/24\), wird policy_A angewendet.

 **Weitere Besonderheiten haben Vorrang vor dem Netzwerk-quintupel.**

Bei Richtlinien Konflikten im Netzwerk-quintupel hat die Richtlinie mit den meisten übereinstimmenden Bedingungen Vorrang. Angenommen, policy_C gibt die Quell-IP-Adresse "Any", die Ziel-IP-Adresse 10.0.0.1, den Quellport "Any", den Zielport "Any" und das Protokoll "TCP" an. 

Nehmen wir als nächstes an, policy_D die Quell-IP-Adresse "Any", die Ziel-IP-Adresse 10.0.0.1, den Quellport "Any", den Zielport 80 und das Protokoll "TCP" angibt. Anschließend policy_C und policy_D beide Verbindungen mit dem Ziel 10.0.0.1:80. Da die QoS-Richtlinie die Richtlinie mit den spezifischsten übereinstimmenden Bedingungen anwendet, hat policy_D in diesem Beispiel Vorrang.  
  
QoS-Richtlinien können jedoch die gleiche Anzahl von Bedingungen aufweisen. Beispielsweise können in mehreren Richtlinien jeweils nur ein Teil des Netzwerk-quintupels angegeben werden. Unter dem Netzwerk-quintupel ist die folgende Reihenfolge von einer höheren zu einer niedrigeren Rangfolge:

- Quell-IP-Adresse

- Ziel-IP-Adresse

- Quellport

- Zielport

- Protokoll (TCP oder UDP)

Innerhalb einer bestimmten Bedingung, wie z. b. IP-Adresse, wird eine spezifischere IP-Adresse mit höherer Rangfolge behandelt. Beispielsweise ist die IP-Adresse 192.168.4.1 spezifischer als 192.168.4.0/24.

Entwerfen Sie Ihre QoS-Richtlinien so speziell wie möglich, um die Fähigkeit Ihrer Organisation zu vereinfachen, welche Richtlinien wirksam sind.

Das nächste Thema in dieser Anleitung finden Sie unter [QoS-Richtlinien Ereignisse und-Fehler](qos-policy-errors.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
