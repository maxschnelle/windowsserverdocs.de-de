---
title: Schritt 2 Konfigurieren der RAS-Server
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0257b98-5633-4264-9df6-b6ffae80592c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a99a2667733c1a23bcba1134d59223044dc000b7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845531"
---
# <a name="step-2-configure-the-remote-access-server"></a>Schritt 2 Konfigurieren der RAS-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, wie Sie die Einstellungen für Client und Server zu konfigurieren, die für die Remoteverwaltung von DirectAccess-Clients erforderlich sind. Bevor Sie die Schritte zur Bereitstellung beginnen, stellen Sie sicher, dass Sie die Planungsschritte, die im Abschnitt abgeschlossen haben [Schritt 2 Planen der Remotezugriffbereitstellung](../plan/Step-2-Plan-the-Remote-Access-Deployment.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Installieren der Remotezugriffsrolle|Installieren Sie die Remotezugriffsrolle.|  
|Konfigurieren des Bereitstellungstypen|Konfigurieren Sie den Bereitstellungstypen als DirectAccess und VPN, nur DirectAccess, oder nur VPN|  
|Konfigurieren von DirectAccess-Clients|Konfigurieren Sie den Remotezugriffsserver mit den Sicherheitsgruppen, die die DirectAccess-Clients enthalten.|  
|Konfigurieren des Remotezugriffsservers|Konfigurieren der Einstellungen des Remotezugriffsservers an.|  
|Konfigurieren des Infrastrukturservers|Konfigurieren Sie die Infrastrukturserver, die in der Organisation eingesetzt werden.|  
|Konfigurieren von Anwendungsservern|Konfigurieren Sie die Anwendungsserver, um die Authentifizierung und-Verschlüsselung benötigen.|  
|Zusammenfassung der Konfiguration und alternative Gruppenrichtlinienobjekte|Zeigen Sie die Zusammenfassung der Remotezugriffskonfiguration an und ändern Sie bei Bedarf die Gruppenrichtlinienobjekte.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Role"></a>Installieren der Rolle "Remotezugriff"  
Sie müssen die Rolle "Remotezugriff" auf einem Server in Ihrer Organisation installieren, die als RAS-Server fungiert.  
  
#### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle  
  
### <a name="to-install-the-remote-access-role-on-directaccess-servers"></a>So installieren Sie die Rolle "Remotezugriff" auf dem DirectAccess-Server  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der **Serverrollen auswählen** die Option **RAS**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf **Weiter** drei Mal.  
  
5.  Auf der **Rollendienste auswählen** die Option **DirectAccess und VPN (RAS)** , und klicken Sie dann auf **Features hinzufügen**.  
  
6.  Wählen Sie **Routing**Option **Web Application Proxy**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
8.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Remote-Access-Server/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="BKMK_Deploy"></a>Konfigurieren des Bereitstellungstypen  
Es gibt drei Optionen, die Sie zum Bereitstellen von Remotezugriff über die Remotezugriffs-Konsole verwenden können:  
  
-   DirectAccess und VPN  
  
-   Nur DirectAccess  
  
-   Nur VPN  
  
> [!NOTE]  
> Diese Anleitung wird die einzige Methode der DirectAccess-Bereitstellung in den Beispielverfahren verwendet.  
  
#### <a name="to-configure-the-deployment-type"></a>So konfigurieren Sie den Bereitstellungstypen  
  
1.  Öffnen Sie auf einem Remotezugriffsserver die Remotezugriffs-Verwaltungskonsole: Auf der **starten** Bildschirm, der Typ, der Typ **Remotezugriffs-Verwaltungskonsole**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im mittleren Bereich auf **Remotezugriffs-Setup-Assistenten ausführen**.  
  
3.  In der **Konfigurieren des Remotezugriffs** (Dialogfeld), wählen DirectAccess und VPN, nur DirectAccess oder nur VPN.  
  
## <a name="BKMK_Clients"></a>Konfigurieren von DirectAccess-clients  
Damit ein Clientcomputer zur Verwendung von DirectAccess bereitgestellt werden kann, muss er zur ausgewählten Sicherheitsgruppe gehören. Nachdem DirectAccess konfiguriert wurde, werden Clientcomputer in der Sicherheitsgruppe bereitgestellt, um die DirectAccess Gruppenrichtlinienobjekte (GPOs) für die Remoteverwaltung zu erhalten.  
  
#### <a name="to-configure-directaccess-clients"></a>So konfigurieren Sie DirectAccess-Clients  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 1 Remoteclients** auf **Konfigurieren**.  
  
2.  In der DirectAccess-Client-Setup-Assistenten auf die **Bereitstellungsszenario** auf **DirectAccess bereitstellen, für die Remoteverwaltung nur**, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Gruppen auswählen** auf **Hinzufügen**.  
  
4.  In der **Gruppen auswählen** Dialogfeld wählen die Sicherheitsgruppen, die die DirectAccess-Clientcomputer enthalten, und klicken Sie dann auf **Weiter**.  
  
5.  Vorgehensweise auf der Seite **Netzwerkkonnektivitäts-Assistent**:  
  
    -   Fügen Sie in der Tabelle die Ressourcen, die verwendet werden, um zu bestimmen, mit dem internen Netzwerk verbunden. Wenn keine weiteren Ressourcen konfiguriert werden, wird automatisch ein Standardwebtest erstellt. Wenn Sie die webtestspeicherorte zum Ermitteln der Konnektivität zum Unternehmensnetzwerk konfigurieren zu können, stellen Sie sicher, dass Sie mindestens eine HTTP-basierten Test konfiguriert haben. Konfigurieren nur einen Pingtest ist nicht ausreichend, und es kann zu einer ungenauen Ermittlung des Verbindungsstatus führen. Dies ist da Ping von IPsec ausgenommen wird. Daher gewährleistet Ping nicht, dass die IPsec-Tunnel ordnungsgemäß eingerichtet werden.  
  
    -   Fügen Sie eine Helpdesk-E-Mail-Adresse hinzu, damit Benutzer Informationen absenden können, wenn bei ihnen Verbindungsprobleme auftreten.  
  
    -   Geben Sie einen Anzeigenamen für die DirectAccess-Verbindung ein.  
  
    -   Aktivieren Sie bei Bedarf das Kontrollkästchen **DirectAccess-Clients ermöglichen, die lokale Namensauflösung zu verwenden**.  
  
        > [!NOTE]  
        > Wenn die lokale namensauflösung aktiviert ist, können Benutzer mit dem Ratgeber für native Kompilierung Auflösen von Namen mithilfe von DNS-Servern, die auf dem DirectAccess-Clientcomputer konfiguriert sind.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Server"></a>Konfigurieren Sie den RAS-server  
Um den Remotezugriff bereitzustellen, müssen Sie den Server zu konfigurieren, der als RAS-Servers durch den folgenden fungiert:  
  
1.  Korrekten Netzwerkadaptern  
  
2.  Eine öffentliche URL für den RAS-Server, für welchen, den Client Computer (die ConnectTo-Adresse) eine Verbindung herstellen können  
  
3.  Ein IP-HTTPS-Zertifikat mit einem Antragsteller, der die ConnectTo-Adresse übereinstimmt.  
  
4.  IPv6-Einstellungen  
  
5.  Clientcomputer-Authentifizierung  
  
#### <a name="to-configure-the-remote-access-server"></a>So konfigurieren Sie den Remotezugriffsserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 2 RAS-Server** auf **Konfigurieren**.  
  
2.  Klicken Sie im Setup-Assistenten für den Remotezugriffsserver auf der Seite **Netzwerktopologie** auf die Bereitstellungstopologie, die in Ihrer Organisation verwendet wird. Geben Sie unter **Geben Sie den öffentlichen Namen oder die öffentliche IPv4-Adresse an** den öffentlichen Namen für die Bereitstellung ein (dieser Name stimmt mit dem Antragstellernamen des IP-HTTPS-Zertifikats überein, z. B. edge1.contoso.com), und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **Netzwerkadapter** Seite der Assistent erkennt automatisch:  
  
    -   Der Netzwerkadapter für die Netzwerke in Ihrer Bereitstellung. Falls der Assistent nicht die korrekten Netzwerkadapter erkennt, wählen Sie die korrekten Adapter manuell aus.  
  
    -   IP-HTTPS-Zertifikat. Dies basiert auf den öffentlichen Namen für die Bereitstellung, die Sie im vorherigen Schritt des Assistenten festlegen. Wenn der Assistent die richtige IP-HTTPS-Zertifikat nicht erkennt, klicken Sie auf **Durchsuchen** das richtige Zertifikat manuell auswählen.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Auf der **Präfixkonfiguration** Seite (diese Seite ist nur sichtbar, wenn IPv6 im internen Netzwerk erkannt wird), erkennt der Assistent automatisch die IPv6-Einstellungen, die auf dem internen Netzwerk verwendet werden. Wenn für Ihre Bereitstellung zusätzliche Präfixe erforderlich sind, konfigurieren Sie die IPv6-Präfixe für das interne Netzwerk, ein IPv6-Präfix zum Zuweisen für DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für VPN-Clientcomputer.  
  
6.  Vorgehensweise auf der Seite **Authentifizierung**:  
  
    -   In Bereitstellungen für mehrere Standorte oder die zweistufige Authentifizierung müssen Sie die Computerzertifikatauthentifizierung verwenden. Wählen Sie die **Computerzertifikate** Kontrollkästchen, um die Computerzertifikatauthentifizierung verwenden, und wählen die IPsec-Stammzertifikat.  
  
    -   Um Windows 7 für die Verbindung über DirectAccess-Clientcomputern zu aktivieren, wählen die **Aktivieren von Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen** Kontrollkästchen. Für diesen Bereitstellungstypen müssen Sie ebenfalls die Computerzertifikatauthentifizierung verwenden.  
  
7.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Infra"></a>Konfigurieren des Infrastrukturservers  
Um die Infrastrukturserver in einer remotezugriffsbereitstellung zu konfigurieren, müssen Sie Folgendes konfigurieren:  
  
-   Netzwerkadressenserver  
  
-   DNS-Einstellungen, einschließlich des DNS-suffix-Suchliste  
  
-   Alle Verwaltungsserver, die nicht automatisch vom Remotezugriff erkannt werden  
  
#### <a name="to-configure-the-infrastructure-servers"></a>So konfigurieren Sie die Infrastrukturserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 3 Infrastrukturserver** auf **Konfigurieren**.  
  
2.  Klicken Sie im Assistenten zum Einrichten des Infrastrukturservers auf der Seite **Netzwerkadressenserver** auf die Option, die dem Speicherort des Netzwerkadressenservers in Ihrer Bereitstellung entspricht.  
  
    -   Wenn der Netzwerkadressenserver auf einem Remotewebserver installiert ist, geben Sie die URL ein, und klicken Sie dann auf **überprüfen** bevor Sie fortfahren.  
  
    -   Wenn der Netzwerkadressenserver nicht auf einem Remotewebserver installiert ist, klicken Sie auf **Durchsuchen**, um das entsprechende Zertifikat zu suchen und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **DNS** Seite in der Tabelle, geben Sie zusätzlichen Namenssuffixe ein, die angewendet werden als Ausnahmen für (Name Resolution Policy Table, NRPT). Wählen Sie die entsprechende Option für die lokale Namensauflösung, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **DNS-Suffixsuchliste** Seite, den Remotezugriffsserver erkennt automatisch die Domänensuffixe in der Bereitstellung. Verwenden Sie die **hinzufügen** und **entfernen** Schaltflächen, um die Liste in der Domänensuffixe zu erstellen, die Sie verwenden möchten. Um ein neues Domänensuffix unter **Neues Suffix** hinzuzufügen, müssen Sie dass Suffix eingeben und anschließend auf **Hinzufügen** klicken. Klicken Sie auf **Weiter**.  
  
5.  Auf der **Management** Seite, Hinzufügen von Verwaltungsservern, die nicht automatisch erkannt werden, und klicken Sie dann auf **Weiter**. Der Remotezugriff fügt die Domänencontroller und System Center Configuration Manager-Server automatisch hinzu.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_App"></a>Konfigurieren von Anwendungsservern  
Beim Konfigurieren von Anwendungsservern in einer vollständigen Remotezugriffs-Bereitstellung ist eine optionale Aufgabe. In diesem Szenario für die Remoteverwaltung von DirectAccess-Clients Anwendungsserver werden nicht verwendet, und dieser Schritt ist abgeblendet, um anzugeben, dass sie nicht aktiv ist. Klicken Sie auf **Fertig stellen** zum Anwenden der Konfiguration.  
  
## <a name="BKMK_GPO"></a>Konfiguration Zusammenfassung und alternative Gruppenrichtlinienobjekte  
Wenn die Konfiguration des Remotezugriffs abgeschlossen ist, wird das Dialogfeld **Überprüfung des Remotezugriffs** angezeigt. Sie können alle zuvor ausgewählten Einstellungen überprüfen, dazu gehören:  
  
-   **GPO-Einstellungen**  
  
    Die DirectAccess-Server-Gruppenrichtlinienobjekt-Namen und die Client-Gruppenrichtlinienobjektname aufgelistet sind. Klicken Sie auf die **Änderung** link die **GPO-Einstellungen** Überschrift, um die GPO-Einstellungen zu ändern.  
  
-   **Remoteclients**  
  
    Die DirectAccess-Clientkonfiguration wird angezeigt, einschließlich der Sicherheitsgruppe, der verbindungsprüfer und der DirectAccess-Verbindungsnamens.  
  
-   **RAS-Server**  
  
    Die DirectAccess-Konfiguration wird angezeigt, einschließlich der öffentliche Name und Adresse, Konfiguration des Netzwerkadapters und Zertifikatinformationen.  
  
-   **Infrastrukturserver**  
  
    Diese Liste enthält die Netzwerkadressenserver-URL, DNS-Suffixe, die von DirectAcccess-Clients verwendet werden sowie Verwaltungsserverinformationen.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Überprüfen der Bereitstellung](Step-3-Verify-the-Deployment_2.md)  
  
  


