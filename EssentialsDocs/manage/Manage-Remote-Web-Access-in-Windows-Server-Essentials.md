---
title: Verwalten des Remotewebzugriffs in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3ea40fa-b6ba-4d66-b754-221ca6271387
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3eace9281d9fcdea5262274ac7fb20ec30d30fb4
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371211"
---
# <a name="manage-remote-web-access-in-windows-server-essentials"></a>Verwalten des Remotewebzugriffs in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Remote Webzugriff in Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle bietet eine optimierte, benutzerfreundliche Browser Darstellung, um von praktisch jedem Standort aus auf Anwendungen und Daten zuzugreifen. Sie verfügen über eine Internet Verbindung und über fast alle Geräte. Damit Sie den Remotewebzugriff verwenden können, müssen Sie ihn zunächst mithilfe des Assistenten zum Einrichten von %%amp;quot;Zugriff überall%%amp;quot; aktivieren und den Router und Domänennamen einrichten.  
  
## <a name="in-this-topic"></a>In diesem Thema  
  
-   [Aktivieren und Konfigurieren von Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Einrichten des Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Einrichten des Domänen Namens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Remote Webzugriff anpassen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [Problembehandlung bei Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_5)  
  
##  <a name="BKMK_1"></a>Aktivieren und Konfigurieren von Remote Webzugriff  
 Die folgenden Themen enthalten hilfreiche Informationen zum Aktivieren und Konfigurieren des Remotewebzugriffs:  
  
-   [Übersicht über Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [Remote Webzugriff einschalten](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA)  
  
-   [Ändern Ihrer Region](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Region)  
  
-   [Verwalten von Remote Webzugriff Berechtigungen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManagePerms)  
  
-   [Sichern von Remote Webzugriff](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SecureRWA)  
  
-   [Remote Webzugriff und VPN-Benutzer verwalten](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ManageRWAVPN)  
  
###  <a name="BKMK_Overview"></a>Übersicht über Remote Webzugriff  
 Wenn Sie nicht im Büro sind, können Sie einen Webbrowser öffnen und von überall aus, der über Internet Zugriff verfügt, auf Remote Webzugriff zugreifen. In Remote Webzugriff können Sie folgende Aktionen ausführen:  
  
- Auf freigegebene Dateien und Ordner auf dem Server zugreifen.  
  
- Auf Server und Computer im Netzwerk zugreifen. Dies bedeutet, dass Sie so auf den Desktop eines Computers im Netzwerk zugreifen können, als säßen Sie am Arbeitsplatz direkt davor.  
  
  Remote Webzugriff ist standardmäßig nicht aktiviert. Wenn Sie den Assistenten für das Einrichten des Zugriffs überall ausführen, versucht der Assistent, den Router und eine Internetverbindung einzurichten. Nachdem der Remote Webzugriff aktiviert wurde, können Sie einen Domänen Namen für Ihren Server einrichten und Remote Webzugriff anpassen. Sie können den Router auch erneut einrichten, wenn Sie den Router wechseln.  
  
  Die Berechtigung für den Zugriff auf Remote Webzugriff wird nicht automatisch gewährt, wenn Sie ein neues Benutzerkonto hinzufügen. Wenn Sie ein Benutzerkonto hinzufügen, können Sie die Berechtigung zum Zugriff auf freigegebene Ordner, die Medienbibliothek, Computer, Links zur Startseite und das Server-Dashboard festlegen. Sie können auch angeben, dass ein Benutzer nicht berechtigt ist, Remote Webzugriff zu verwenden.  
  
  Die Remote Webzugriff Einstellung wird für jedes Benutzerkonto auf der Registerkarte " **Benutzer** " des Windows Server Essentials-Dashboards angezeigt. Zum Ändern der Einstellung für den Remote Webzugriff klicken Sie mit der rechten Maustaste auf das Benutzerkonto, und klicken Sie dann auf **Konto Eigenschaften anzeigen**.  
  
###  <a name="BKMK_TurnOnRWA"></a>Remote Webzugriff einschalten  
 Sie können den Remotewebzugriff aktivieren, indem Sie im Serverdashboard den Assistenten zum Einrichten von %%amp;quot;Zugriff überall%%amp;quot; ausführen.  
  
##### <a name="to-turn-on-remote-web-access"></a>So aktivieren Sie den Remotewebzugriff  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
3.  Klicken Sie auf **Konfigurieren**. Der Assistent zum Einrichten von %%amp;quot;Zugriff überall%%amp;quot; wird gestartet.  
  
4.  Aktivieren Sie auf der Seite **Folgende Funktionen für " Zugriff überall" aktivieren** das Kontrollkästchen **Remotewebzugriff**.  
  
5.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
###  <a name="BKMK_Region"></a>Ändern Ihrer Region  
 Sie müssen Netzwerkadministrator sein, um die Einstellung der Region in Windows Server Essentials zu ändern.  
  
##### <a name="to-change-the-region-setting"></a>So ändern Sie die Einstellung der Region  
  
1.  Öffnen Sie das Dashboard auf einem Computer, der mit Windows Server Essentials verbunden ist.  
  
2.  Klicken Sie auf **Einstellungen**.  
  
3.  Klicken Sie auf der Registerkarte **Allgemein** auf die Dropdownliste im Abschnitt **Land/Region des Servers**.  
  
4.  Wählen Sie in der Dropdownliste die neue Region aus, und klicken Sie dann auf **Übernehmen**, um die neue Regionseinstellung zu bestätigen.  
  
###  <a name="BKMK_ManagePerms"></a>Verwalten von Remote Webzugriff Berechtigungen  
 Wenn Sie ein Benutzerkonto in Windows Server Essentials hinzufügen, ist der neue Benutzer standardmäßig berechtigt, den Remotewebzugriff zu verwenden. Wenn Sie sich entschieden haben, Remote Webzugriff für ein Benutzerkonto zuzulassen und dann festzustellen, dass der Benutzer Remote Webzugriff verwenden muss, können Sie die Eigenschaften des Benutzerkontos aktualisieren.  
  
##### <a name="to-manage-remote-web-access-permissions-for-a-user-account"></a>So verwalten Sie den Remotewebzugriff für ein Benutzerkonto  
  
1. Melden Sie sich beim Dashboard an, und klicken Sie dann auf **Benutzer**.  
  
2. Klicken Sie auf das Benutzerkonto, das Sie verwalten möchten, und klicken Sie anschließend auf **Kontoeigenschaften anzeigen** im Bereich **Aufgaben**.  
  
3. Klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Zugriff überall**.  
  
4. Aktivieren Sie auf der Registerkarte **Zugriff überall** das Kontrollkästchen **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**, damit der Benutzer eine Verbindung zum Server über den Remotewebzugriff herstellen kann.  
  
5. Klicken Sie auf **Übernehmen** und dann auf **OK**.  
  
   Weitere Informationen finden Sie unter [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
###  <a name="BKMK_SecureRWA"></a>Sichern von Remote Webzugriff  
 Windows Server Essentials verwendet ein Sicherheitszertifikat zum Sichern der Informationen, die zwischen der Software und einem Webbrowser ausgetauscht werden. Wenn Sie die Connector-Software auf Ihren Computern installieren, wird das Sicherheitszertifikat für Windows Server Essentials der Liste der vertrauenswürdigen Zertifikate auf Ihren Computern hinzugefügt. Die beste Möglichkeit für Benutzer, den Remotewebzugriff zu verwenden, wenn sie nicht im Büro sind, ist die Nutzung eines tragbaren Computers, auf dem die Connector-Software installiert ist.  
  
> [!WARNING]
>  Benutzer, die den Remotewebzugriff von öffentlichen Standorten oder anderen nicht vertrauenswürdigen Computern aus verwenden, sollten sicherstellen, dass sie sich von der Website abmelden, bevor sie den Computer unbeaufsichtigt lassen oder wenn sie ihre Sitzung beendet haben.  
  
###  <a name="BKMK_ManageRWAVPN"></a>Remote Webzugriff und VPN-Benutzer verwalten  
 Sie können eine Verbindung mit Windows Server Essentials über VPN herstellen und auf alle Ressourcen zugreifen, die auf dem Server gespeichert sind. Dies ist besonders dann nützlich, wenn auf Ihrem Clientcomputer Netzwerkkonten eingerichtet sind, die verwendet werden können, um eine Verbindung mit einem gehosteten Windows Server Essentials-Server über eine VPN-Verbindung herzustellen. Alle auf dem dem gehosteten Windows Server Essentials-Server neu erstellten Benutzerkonten müssen bei der ersten Anmeldung am Clientcomputer VPN verwenden.  
  
##### <a name="to-set-vpn-and-remote-web-access-permissions-for-network-users"></a>So richten Sie VPN- und Remotewebzugriff-Berechtigungen für Benutzer im Netzwerk ein  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf der Navigationsleiste auf **BENUTZER**.  
  
3.  Wählen Sie in der Liste von Benutzerkonten das Benutzerkonto aus, für das Sie die Berechtigung zum Remotezugriff auf den Desktop gewähren möchten.  
  
4.  Klicken Sie im Bereich **< Benutzerkonto\> Tasks** auf **Eigenschaften**.  
  
5.  Klicken Sie in **< Eigenschaften von Benutzerkonto\>** auf die Registerkarte **Zugriff überall** .  
  
6.  Gehen Sie auf der Registerkarte **Zugriff überall** in folgender Weise vor:  
  
    1.  Um dem Benutzer die Berechtigung zu gehören, eine Verbindung zum Server über VPN herzustellen, aktivieren Sie das Kontrollkästchen **Virtuelles privates Netzwerk (VPN) zulassen**.  
  
    2.  Um einem Benutzer die Herstellung einer Verbindung zum Server über den Remotewebzugriff zu erlauben, aktivieren Sie das Kontrollkästchen **Remotewebzugriff und Zugriff auf Webdienstanwendungen zulassen**.  
  
7.  Klicken Sie auf **Übernehmen** und dann auf **OK**.  
  
##  <a name="BKMK_2"></a>Einrichten des Routers  
 Beim Konfigurieren des Servers für den Remotewebzugriff versucht der Assistent zum Einrichten von "Zugriff überall" den Router einzurichten. Wenn Sie die Router oder Einstellungen des Routers ändern, muss der Assistent zum Einrichten des Routers erneut ausgeführt werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Einrichten des Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpRouter)  
  
-   [Ersetzen eines Routers](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ReplaceRouter)  
  
-   [Netzwerk Speicherort definiert](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_NetworkLocation)  
  
-   [Aktivieren von Remotedesktopdienste ActiveX-Steuerelementen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ActiveX)  
  
###  <a name="BKMK_SetUpRouter"></a>Einrichten des Routers  
 In diesem Schritt versucht Windows Server Essentials, den Router anhand von UPnP-Befehlen automatisch zu konfigurieren. Dazu muss der Router UPnP-Standards unterstützen, und die UPnP-Einstellung muss auf dem Router aktiviert sein.  
  
> [!NOTE]
>  Die Netzwerkverbindung sollte die unterstützte Netzwerkanforderung für Windows Server Essentials erfüllen. Im Netzwerk sollte nur ein Router vorhanden sein.  
  
 Wenn der Router nicht mit dem Assistenten zum Einrichten des Domänennamens eingerichtet wurde, müssen Sie Port 443 manuell weiterleiten. Informationen zum Einrichten der Portweiterleitung auf dem Router finden Sie unter [Router Setup](https://social.technet.microsoft.com/wiki/contents/articles/windows-small-business-server-2011-essentials-router-setup.aspx).  
  
###  <a name="BKMK_ReplaceRouter"></a>Ersetzen eines Routers  
 Ersetzen Sie den Router gemäß den Anweisungen des Herstellers, und führen Sie dann den Assistenten zum Einrichten des Routers aus, um den neuen Router zu konfigurieren.  
  
##### <a name="to-set-up-your-new-router"></a>So richten Sie den neuen Router ein  
  
1.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf **Einstellungen**.  
  
2.  Klicken Sie auf die Registerkarte **Zugriff überall**, und klicken Sie dann im Abschnitt **Router** auf **Einrichten**. Der Assistent zum Einrichten des Routers wird gestartet.  
  
3.  Folgen Sie den Anweisungen im Assistenten, um das Einrichten des neuen Routers fertigzustellen.  
  
###  <a name="BKMK_NetworkLocation"></a>Netzwerk Speicherort definiert  
 Eine Netzwerkadresse ist eine Sammlung von Netzwerkeinstellungen, die von Windows angewendet werden, wenn Sie sich mit einem Netzwerk verbinden. Die Einstellungen variieren und können basierend auf dem Typ des Netzwerks, das Sie verwenden, angepasst werden. Die Einstellungen für eine Netzwerkadresse bestimmen, ob bestimmte Features (z. B. Datei- und Druckerfreigabe, Netzwerkerkennung und Freigabe öffentlicher Ordner) aktiviert oder deaktiviert werden. Netzwerkadressen sind nützlich, wenn Sie eine Verbindung mit unterschiedlichen Netzwerken herstellen müssen.  
  
 Sie können beispielsweise einen Laptop besitzen, den Sie zu Hause und bei der Arbeit verwenden. Wenn Sie im Büro sind, verbinden Sie sich mit dem Firmennetzwerk. Wenn Sie aber nach Hause können, verwenden Sie den Laptop, um auf Videos und Musik zuzugreifen, die auf dem Heimserver gespeichert sind. Wenn Sie eine Verbindung mit einem neuen Netzwerk herstellen und den Adressenart angeben, weist Windows ein Netzwerkprofil zu, das für diese Adressenart voreingestellt ist. Beim nächsten Herstellen einer Verbindung mit diesem Netzwerk erkennt Windows das Netzwerk und weist automatisch die richtigen Einstellungen zu. Dadurch wird eine weitere Sicherheitsebene zum Schutz der Informationen auf Ihrem Computer hinzugefügt, und nur die Netzwerkfeatures, die Sie für diesen Speicherort benötigen, werden aktiviert.  
  
 Es gibt vier Arten von Netzwerkadressen:  
  
-   **Heimnetzwerk** Wählen Sie dieses Netzwerk für Heimnetzwerke oder wenn Sie die Personen und Geräte im Netzwerk kennen und für vertrauenswürdig halten. Computer in einem Heimnetzwerk können einer Heimnetzgruppe angehören. Die Netzwerkerkennung, mit der Sie andere Computer und Geräte im Netzwerk anzeigen und andere Benutzer im Netzwerk Ihren Computer sehen können, ist für Heimnetzwerke aktiviert.  
  
-   **Firmennetzwerk** Wählen Sie dieses Netzwerk für kleine Firmennetzwerke oder andere Arbeitsplatznetzwerke aus. Die Netzwerkerkennung, mit der Sie andere Computer und Geräte im Netzwerk anzeigen und andere Benutzer im Netzwerk Ihren Computer sehen können, ist standardmäßig aktiviert.  
  
-   **Öffentliches Netzwerk** Wählen Sie dieses Netzwerk für öffentliche Orte (z. b. Kaffee Geschäfte oder Flughäfen) aus. Diese Netzwerkadresse verhindert, dass der Computer für andere Computer in der Umgebung sichtbar ist. Außerdem trägt sie dazu bei, den Computer vor Schadsoftware aus dem Internet zu schützen. Die Heimnetzgruppe ist in öffentlichen Netzwerken nicht verfügbar, und die Netzwerkerkennung ist deaktiviert. Sie sollten diese Option auch auswählen, wenn Sie ohne Verwendung eines Routers direkt mit dem Internet verbunden sind, oder wenn Sie eine mobile Breitbandverbindung verwenden.  
  
-   **Domäne** Wählen Sie dieses Netzwerk für Domänennetzwerke aus, wie sie beispielsweise an Arbeitsplätzen in Unternehmen zu finden sind. Diese Art von Netzwerkadresse wird vom zuständigen Netzwerkadministrator gesteuert und kann nicht ausgewählt oder geändert werden.  
  
###  <a name="BKMK_ActiveX"></a>Aktivieren von Remotedesktopdienste ActiveX-Steuerelementen  
 Mit den Remotedesktopdienste ActiveX-Steuerelementen können Sie über das Internet über das Internet über das Internet auf Ihren Heim-oder Geschäftscomputer zugreifen, indem Sie Remote Webzugriff verwenden.  
  
##### <a name="to-enable-remote-desktop-services-activex-controls"></a>So aktivieren Sie die ActiveX-Steuerelemente für Remotedesktopdienste  
  
1.  Klicken Sie in Internet Explorer auf **Extras**, und klicken Sie dann auf **Internetoptionen**.  
  
2.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Stufe anpassen**.  
  
3.  Gehen Sie im Abschnitt **ActiveX-Steuerelemente und Plugins** wie folgt vor:  
  
    1.  Klicken Sie unter **Download von signierten ActiveX-Steuerelementen** auf **Bestätigen**.  
  
    2.  Klicken Sie unter **ActiveX-Steuerelemente und Plugins ausführen** auf **Aktivieren**.  
  
4.  Klicken Sie zweimal auf **OK**, um die Änderungen zu übernehmen und das Dialogfeld zu schließen.  
  
##  <a name="BKMK_3"></a>Einrichten des Domänen Namens  
 Nach dem Aktivieren des Remotewebzugriffs können Sie einen Domänennamen für den Server mit Windows Server Essentials einrichten. Dieser Schritt ist erforderlich, wenn Sie den Remotewebzugriff auf einem Remotecomputer verwenden möchten. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Übersicht über Domänen Namen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_DNOverview)  
  
-   [Informationen zu persönlichen Microsoft-Domänen Namen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_PersonalizedNames)  
  
-   [Neuen oder vorhandenen Domänen Namen verwenden](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UseNewName)  
  
-   [Einrichten eines Domänen Namens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetUpName)  
  
-   [Wählen Sie einen Domain Name Service-Anbieter aus.](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseProvider)  
  
-   [Domänen Namen auswählen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ChooseDomainName)  
  
-   [Auswählen eines Domänen Namen Präfixes](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Prefixes)  
  
-   [Domänen Namen Erweiterung auswählen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Extension)  
  
-   [Aktualisieren oder Aktualisieren Ihres Domain Name Service](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UpdateService)  
  
-   [Exportieren oder Importieren Ihres Zertifikats auf dem Server](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ExportCert)  
  
-   [Manuelles Einrichten eines Domänen Namens](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SetNameManually)  
  
-   [Suchen Ihres Domain Name Service-Anbieters](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Find)  
  
###  <a name="BKMK_DNOverview"></a>Übersicht über Domänen Namen  
 Ein Domänennamen identifiziert Ihren Server im Internet eindeutig. Domänennamen bestehen aus mindestens zwei Teilen: einem Domänennamen der obersten Ebene (TLD, Top Level Domain) und einem Domänennamen der zweiten Ebene In contoso.com ist com z. b. die TLD, und der Domänen Name der zweiten Ebene ist.  
  
 Wenn Sie nicht im Büro sind, können Sie Ihren Domänennamen verwenden, um auf freigegebene Dateien auf dem Server oder auf Computern im Netzwerk zuzugreifen. Sie können Ihren Server auch verwalten, wenn Sie nicht am Arbeitsplatz sind. Sie können beispielsweise "contoso.com" für den Server registrieren. Wenn Sie nicht im Büro sind, können Sie einen Webbrowser auf Ihrem Laptop öffnen und **contoso.com** in das Adressentextfeld eingeben, um eine Verbindung mit der Instanz des Remotewebzugriffs herzustellen, die auf Windows Server Essentials eingerichtet ist.  
  
###  <a name="BKMK_PersonalizedNames"></a>Informationen zu persönlichen Microsoft-Domänen Namen  
 Ein personalisierter Microsoft-Domänenname umfasst die folgenden Features:  
  
- Ein benutzerdefinierter Domänen Name für Remote Webzugriff (z. b. *ihrhostname*. remotewebaccess.com). Ihr Domänenname ist Ihrer öffentlichen IP-Adresse zugeordnet.  
  
- Ein DNS-Protokolldienst für das dynamische Update, damit Remote Webzugriff mit Ihrem Domänen Namen nicht unterbrochen werden, wenn sich Ihre öffentliche IP-Adresse ändert. In der Regel stellen Internet Dienstanbieter (ISPs) für die Breitbandverbindungen Ihrer Organisation dynamische öffentliche IP-Adressen bereit, die sich ändern können.  
  
- Ein vertrauenswürdiges Zertifikat, das mit dem Domänennamen verknüpft ist.  
  
  Um einen persönlichen Microsoft-Domänennamen mit Ihrem Server zu integrieren, benötigen Sie ein Microsoft-Konto (früher bekannt als Windows Live ID). Wenn Sie kein Microsoft-Konto haben, können Sie sich auf der [Microsoft Hotmail](https://login.live.com/) -Website anmelden, um sich für ein Konto zu registrieren.  
  
> [!IMPORTANT]
>  Windows Live erlaubt die Verwendung von Sonderzeichen in Ihrem Microsoft-Konto-Kennwort, die der Server nicht unterstützt. Stellen Sie bei Verwendung einer personalisierten Microsoft-Domäne sicher, dass das Kennwort für Ihr Microsoft-Konto nur Zeichen enthält, die der Server unterstützt. Der Server unterstützt die Verwendung der Zeichen $, /, ' und % nicht.  
  
###  <a name="BKMK_UseNewName"></a>Neuen oder vorhandenen Domänen Namen verwenden  
 Um den Namen Ihrer Domäne auf einem Server unter Windows Server Essentials automatisch einzurichten, müssen Sie einen Domain Name Service-Anbieter verwenden, die im Assistenten zum Einrichten von Domänennamen aufgeführt ist. Sie können einen neuen Domänennamen auswählen oder einen vorhandenen Domänennamen verwenden. Führen Sie eine der folgenden Aktionen aus:  
  
-   Wenn Sie von einem der im Assistenten aufgeführten Domain Name Service-Anbieter einen neuen Domänennamen erhalten möchten, klicken Sie auf **Ich möchte einen neuen Domänennamen einrichten**.  
  
-   Wenn Sie einen vorhandenen Domänennamen haben, den Sie von einem der unterstützten Domain Name Service-Anbieter erworben haben, können den Assistenten zum Einrichten von Domänennamen verwenden, um den Domänennamen für den Server einzurichten. Klicken Sie auf **Ich möchte einen Domänennamen verwenden, den ich bereits besitze**, und geben Sie dann den Domänennamen in das Textfeld **Domänennamen einrichten** ein. Sie müssen den Benutzernamen und das Kennwort angeben, die Sie zum Erwerb des Domänennamens verwendet haben.  
  
-   Wenn Sie über einen vorhandenen Domänennamen verfügen, den Sie von einem Domain Name Service-Anbieter erworben haben, der nicht von Windows Server Essentials unterstützt wird, und Sie den Assistenten zum Einrichten von Domänennamen für den Server verwenden möchten, können Sie den Domänennamen zu einem der im Assistenten aufgeführten Domain Name Service-Anbieter übertragen. Klicken Sie auf **Ich möchte einen Domänen Namen verwenden, den ich bereits besitze**, geben Sie den Domänen Namen in das Textfeld **Domänen Name** ein, und befolgen Sie dann die Anweisungen auf der Website des Domänen Namen Dienstanbieters, um den Domänen Namen  
  
###  <a name="BKMK_SetUpName"></a>Einrichten eines Domänen Namens  
 Beim Einschalten des Remotewebzugriffs können Sie wählen, dass Sie den Internetdomänennamen des Servers einrichten.  
  
##### <a name="to-set-up-or-manage-an-internet-domain-name"></a>So richten Sie einen Internetdomänennamen ein oder verwalten diesen  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Servereinstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
3.  Klicken Sie im Abschnitt **Domänennamen** auf **Einrichten**.  
  
4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen. Wenn Sie noch keinen Domänennamen und kein Zertifikat besitzen, unterstützt Sie der Assistent dabei, einen Domain Name Service-Anbieter und ein Zertifikat zu erwerben. Sie können auch einen personalisierten Microsoft-Domänennamen erhalten.  
  
###  <a name="BKMK_ChooseProvider"></a>Wählen Sie einen Domain Name Service-Anbieter aus.  
 Sie sollten einen Domain Name Service-Anbieter auswählen, der die Domänennamenerweiterung unterstützt, die Sie verwenden möchten. Der Assistent zum Einrichten des Domänen namens umfasst eine Liste qualifizierter Anbieter, die Sie mit einem Link zur Website jedes Anbieters verwenden können. Klicken Sie auf den Link **Weitere Informationen** neben dem Namen des Anbieters, um Informationen zu den Diensten und Preisen des Anbieters zu erhalten.  
  
> [!NOTE]
>  Einige Domain Name Service-Anbieter bedienen international breite Regionen, während andere in kleineren Märkten tätig sind. Daher bieten möglicherweise nicht alle Anbieter eine Website an, die in die von Ihnen bevorzugte Sprache übersetzt ist.  
  
 Beim Erwerb Ihres Domänennamens sollten Sie auch den Erwerb des Protokolldiensts für dynamische DNS-Updates von Ihrem Domain Name Service-Anbieter in Betracht ziehen. Das Protokoll für dynamische DNS-Updates ist ein Dienst, der es ermöglicht, dass alle Benutzer im Internet auf Ressourcen in einem lokalen Netzwerk zugreifen können, wenn sich die IP-Adresse des Netzwerks ständig ändert. Sie können alternativ dazu auch eine statische IP-Adresse von Ihrem Internetdienstanbieter (ISP) erwerben, um sicherzustellen, dass sich Ihre IP-Adresse nicht ändert.  
  
###  <a name="BKMK_ChooseDomainName"></a>Domänen Namen auswählen  
 Wählen Sie einen Namen, der Ihren Geschäftssserver eindeutig identifiziert. Beispiel: Wenn Ihr Unternehmen den Namen Contoso Ltd hat, könnten Sie Contoso wählen, um Ihren Heim- oder Geschäftsserver im Internet eindeutig zu identifizieren. Wenn der Domänenname nicht verfügbar ist, probieren Sie eine Variante dieses Namens aus, oder wählen Sie einen ganz anderen Namen.  
  
 Der eingegebene Name kann Folgendes enthalten:  
  
-   Maximale Länge 63 Zeichen  
  
-   Buchstaben (englische oder lokalisierte Zeichen), Ziffern oder Bindestriche (-). Der Name muss mit einem Buchstaben oder einer Zahl beginnen und enden.  
  
    > [!NOTE]
    >  Bei Domänennamen wird die Groß-/Kleinschreibung nicht beachtet.  
  
###  <a name="BKMK_Prefixes"></a>Auswählen eines Domänen Namen Präfixes  
 Ein Domänenname besteht aus hierarchischen Bezeichnungen.  
  
 **Der Domänennamenerweiterung der obersten Ebene** steht ganz rechts im Domänennamen. Beispielsweise ist com in www\.contoso.com die Domänen Namen Erweiterung der obersten Ebene.  
  
 **Der Domänenname der zweiten Ebene** ist die Bezeichnung neben der Domänennamenerweiterung auf oberster Ebene. Der Domänenname der zweiten Ebene wird häufig auf der Basis von Firmennamen, Produkten oder Dienstleistungen erstellt. Beispielsweise handelt es sich bei "www\.contoso.com" um den Domänen Namen der zweiten Ebene und wurde für den Firmennamen "mso Pharmaceuticals" ausgewählt. Dem Domänennamen der zweiten Ebene, manchmal als Hostname bezeichnet, ist eine IP-Adresse zugeordnet.  
  
 **Das Domänennamenpräfix** identifiziert eine Unterdomäne. Der Name der Unterdomäne kann verwendet werden, um Dienste, Geräte oder Regionen zu identifizieren. Beispiel: Contoso Pharmaceuticals möchte Remotebenutzern erlauben, dass sie sich mit den Remotewebzugriff anmelden, möchte jedoch die Website nicht für die Öffentlichkeit verfügbar machen. Daher erstellt das Unternehmen eine Unterdomäne, die nur Benutzern mit den entsprechenden Berechtigungen den Zugriff auf die Website erlaubt. Contoso Pharmaceuticals richtet "remote.contoso.com" als die Unterdomäne ein, wobei "remote" das Domänennamenpräfix ist.  
  
> [!TIP]
>  Es wird empfohlen, die standardmäßige Bezeichnung **Remote** als Präfix für den Domänennamen zu verwenden.  
  
###  <a name="BKMK_Extension"></a>Domänen Namen Erweiterung auswählen  
 Wenn Sie einen Domänennamen für Ihre Website auswählen, müssen Sie auch die Domänennamenerweiterung angeben, die Sie verwenden möchten. Bei dieser Erweiterung handelt es sich um die Buchstaben nach dem letzten Punkt in einem Domänennamen. (Der formale Begriff für die Erweiterung ist die Domäne der obersten Ebene oder TLD.)  
  
 Es gibt zwei Haupttypen von Domänenerweiterungen: allgemeine Erweiterungen und auf dem Ländercode basierende Erweiterungen.  
  
#### <a name="generic-top-level-domains"></a>Allgemeine Domänen der obersten Ebene  
 Allgemeine Domänenerweiterungen sind mindestens drei Buchstaben lang; sie werden in erster Linie von bestimmten Typen von Organisationen genutzt.  
  
 **Beispiele für allgemeine Domänen der obersten Ebene**  
  
|Domänenerweiterung|Beschreibung|  
|----------------------|-----------------|  
|.com|Wird in der Regel von kommerziellen Organisationen verwendet, steht aber zur Verwendung frei.|  
|.net|Speziell für Unternehmen, die Netzwerkinfrastrukturdienste anbieten.|  
|.org|Wurde ursprünglich von gemeinnützigen Organisationen und anderen Unternehmen verwendet, die nicht unter eine andere Kategorie der allgemeinen Domänen der obersten Ebene fielen. Kann von beliebigen Benutzern verwendet werden.|  
|.edu|Beschränkt auf die Verwendung durch Ausbildungseinrichtungen.|  
  
#### <a name="country-code-top-level-domains"></a>Domänen der obersten Ebene auf Ländercodeebene  
 Diese Domänen umfassen zwei Buchstaben. Sie sollen von Organisationen im Land oder in der Region verwendet werden, das bzw. die dem Code zugewiesen ist. Manche Domänen der obersten Ebene auf Ländercodeebene sind auf die Verwendung durch Angehörige des Landes oder der Region beschränkt. Andere können von beliebigen Benutzern verwendet werden.  
  
 **Beispiele für Domänen der obersten Ebene auf Ländercode Ebene**  
  
|Domänenerweiterung|Beschreibung|  
|----------------------|-----------------|  
|.ca|Für die Verwendung durch Websites in Kanada|  
|.cn|Für die Verwendung durch Websites in China|  
|.de|Für die Verwendung durch Websites in Deutschland|  
|.co.uk|Für die Verwendung durch Websites im Vereinigten Königreich|  
  
 Eine vollständige Liste der Domänen der obersten Ebene finden Sie auf der Website [Internet Assigned Numbers Authority](https://go.microsoft.com/fwlink/?LinkId=117438).  
  
#### <a name="if-a-domain-extension-is-not-available-to-select-in-the-set-up-domain-name-wizard"></a>Vorgehensweise, wenn eine Domänenerweiterung im Assistenten zum Einrichten von Domänennamen nicht verfügbar ist  
 Beim Ausführen des Assistenten zum Einrichten von Domänennamen werden zur Bestimmung von Land oder Region die Systeminformationen überprüft. Der Assistent zeigt dann nur die Domänenerweiterungen an, die die teilnehmenden Anbieter in Ihrer Region unterstützen. Wenn die gewünschte Domänenerweiterung nicht in der Liste erscheint, müssen Sie eine andere Domänenerweiterung wählen, um fortzufahren. Wählen Sie eine Erweiterung aus der Liste der vom Assistenten zurückgegebenen Erweiterungen aus.  
  
###  <a name="BKMK_UpdateService"></a>Aktualisieren oder Aktualisieren Ihres Domain Name Service  
 Möglicherweise müssen Sie ein Update oder Upgrade Ihres Domain Name Service durchführen, wenn Sie einen Domänennamen, jedoch kein Zertifikat erworben haben. Sie müssen von Ihrem Domain Name Service-Anbieter ein Zertifikat für Ihren Domänennamen erwerben.  
  
> [!NOTE]
>  Ermitteln Sie in Zusammenarbeit mit Ihrem Domain Name Service-Anbieter den Typ des Zertifikats, den Sie benötigen. Das Zertifikat kann eines der angebotenen kostengünstigen Zertifikate sein. Sie sollten jedoch die Dokumentation und die Features von Zertifikaten mit einer höheren Sicherheitsstufe prüfen, um festzustellen, ob diese die Anforderungen Ihres Unternehmens besser erfüllen.  
  
###  <a name="BKMK_ExportCert"></a>Exportieren oder Importieren Ihres Zertifikats auf dem Server  
 Wenn Sie eine Sicherungskopie eines Zertifikats erstellen oder dieses auf einen anderen Server verwenden möchten, müssen Sie das Zertifikat exportieren. Informationen zum Exportieren von Zertifikaten finden Sie unter [Exportieren eines Zertifikats](https://go.microsoft.com/fwlink/p/?LinkId=214362).  
  
###  <a name="BKMK_SetNameManually"></a>Manuelles Einrichten eines Domänen Namens  
 Wenn Sie diese Option auswählen, überwacht und verwaltet der Server Ihren Domänenname nicht, und Sie werden nicht benachrichtigt, wenn ein Konfigurationsproblem vorliegt. Sie können diese Option auch in Betracht ziehen, wenn einer der folgenden Fälle zutrifft:  
  
- Für Ihr Land bzw. Ihre Region sind keine Partneranbieter für Domänennamen aufgeführt.  
  
- Ihre Domänennamenerweiterung wird von den aufgeführten Partnerdomänenanbietern nicht unterstützt.  
  
- Der vorhandene Domänenname stammt von einem Domänennamenanbieter, der derzeit kein Partner ist, und Sie möchten diesen Domänennamen nicht an einen von Windows Server Essentials unterstützten Domänennamenanbieter übertragen.  
  
- Im Assistenten ist die Domänennamenerweiterung, die Sie verwenden möchten, nicht aufgeführt. Die Erweiterung ist jedoch von einem Domänennamenanbieter verfügbar, der derzeit kein Partner ist.  
  
  Wenn Sie den Domänen Namen manuell einrichten möchten, wenden Sie sich an Ihren Domain Name Service-Anbieter, um einen A-Datensatz für Ihre Domäne zu erstellen.  
  
##### <a name="to-create-an-a-record"></a>So erstellen Sie einen A-Datensatz  
  
1.  Entscheiden Sie sich für einen Hostnamen, z. b. Remote. Dies ist das Domänennamenpräfix. Mit dem Domänen Namen Präfix und dem Domänen Namen wird die URL zum Öffnen der Remote Webzugriff-Anmeldeseite definiert. beispielsweise **http://remote.contoso.com** .  
  
2.  Erstellen Sie im Konfigurations Dashboard ihres Domänen Namen Dienstanbietern (in der Regel auf der Webseite) den A-Datensatz für den Hostnamen, den Sie in Schritt 1 ausgewählt haben. Stellen Sie sicher, dass die IP-Adresse, die Sie im A-Datensatz angeben, die IP-Adresse auf der WAN-Seite des Routers (die Seite mit Internet Zugriff) ist. Die WAN-IP-Adresse finden Sie in der Routerdokumentation.  
  
3.  Es wird empfohlen, vom Internetdienstanbieter eine statische IP-Adresse für Ihr Netzwerk zu erwerben. Dadurch wird sichergestellt, dass sich die IP-Adresse nicht ändert und der DNS-Eintrag immer aktuell ist.  
  
     Wenn keine Möglichkeit besteht, eine statische IP-Adresse vom Internetdienstanbieter zu erhalten, können Sie auch den Protokolldienst für dynamische DNS-Updates vom Domain Name Service-Anbieter oder einem anderen Dienstanbieter erwerben. Beim Protokoll für dynamische DNS-Updates handelt es sich um einen Dienst, mit dem die WAN-IP-Adresse für Ihr Netzwerk auf dem neuesten Stand gehalten wird, sodass die IP-Adresse in Ihren Domänennamen aufgelöst werden kann, auch wenn sich die IP-Adresse ändert.  
  
4.  Importieren Sie ein vertrauenswürdiges Zertifikat, wenn Sie vom Assistenten dazu aufgefordert werden. Verfügen Sie nicht über ein vertrauenswürdiges Zertifikat, können Sie eins von einem der im Assistenten aufgeführten unterstützten Domänennamenanbieter oder einem vertrauenswürdigen Anbieter Ihrer Wahl erwerben. Weitere Informationen zu vertrauenswürdigen Zertifikaten erhalten Sie von Ihrem Domänennamenanbieter.  
  
###  <a name="BKMK_Find"></a>Suchen Ihres Domain Name Service-Anbieters  
  
##### <a name="to-find-the-domain-name-service-provider-for-your-domain-name"></a>So finden Sie den Domain Name Service-Anbieter für Ihren Domänennamen  
  
1. Öffnen Sie einen Webbrowser, und geben Sie in die Adressleiste <strong>www.internic.com</strong> ein, um zur Startseite von Internic zu gelangen.  
  
2. Klicken Sie auf der Startseite von Internic auf **Whois**.  
  
3. Geben Sie in das Feld **Whois** den Namen Ihrer Domäne ein (z. B. "contoso.com").  
  
4. Klicken Sie auf die Option **Domäne**, und klicken Sie dann auf **Absenden**.  
  
5. Der Name des Domain Name Service-Anbieter wird in den Suchergebnissen unter **Registrierungsstelle** aufgeführt.  
  
##  <a name="BKMK_4"></a>Remote Webzugriff anpassen  
 Sie können die Remotewebzugriffssite mit einem persönlichen Logo oder Hintergrundbild anpassen. Sie können auch Links auf der Startseite hinzufügen, sodass diese Informationen allen Benutzern zur Verfügung stehen. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Remote Webzugriff anpassen](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeRWA)  
  
-   [Anpassen von Bildern für Hintergründe und Logos](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_CustomizeImages)  
  
-   [Remote Webzugriff reparieren](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_RepairRWA)  
  
###  <a name="BKMK_CustomizeRWA"></a>Remote Webzugriff anpassen  
 Sie können den Remotewebzugriff anpassen, indem Sie den Titel der Website, das Hintergrundbild und das Logo ändern und Links zu anderen Websites auf der Startseite hinzufügen.  
  
##### <a name="to-customize-remote-web-access"></a>So passen Sie den Remotewebzugriff an  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
3.  Klicken Sie im Abschnitt **Websiteeinstellungen** auf **Anpassen**.  
  
4.  Wenn Sie mit dem Anpassen des Remotewebzugriffs fertig sind, klicken Sie auf **OK**. Testen Sie die am Remotewebzugriff vorgenommenen Änderungen.  
  
###  <a name="BKMK_CustomizeImages"></a>Anpassen von Bildern für Hintergründe und Logos  
 Dieser Abschnitt enthält Informationen zu den Bildern, die Sie zum Anpassen des Remotewebzugriffs verwenden können.  
  
#### <a name="image-size"></a>Bildgröße  
 **Logo Bilder**  
  
 Es wird empfohlen, Logos mit einer Größe von 32 x 32 Pixel zu verwenden. Größere Bilder werden auf 32 x 32 verkleinert und kleinere Bilder werden auf 32 x 32 gedehnt. Dadurch könnte das Bild verzerrt werden.  
  
 **Hintergrundbilder**  
  
 Es gibt zwar keine Größenbeschränkung für Hintergrundbilder, aber es empfiehlt sich, Bilder mit einer Größe von ca. 800 x 500 Pixel zu verwenden, um die besten Ergebnisse zu erhalten. Das Hintergrundbild wird in der Mitte (vertikal und horizontal) der Anmeldeseite platziert. Damit der Text auf der Anmeldeseite einfacher lesbar ist, sollte die Mitte des Hintergrundbildes eine helle Farbe haben.  
  
#### <a name="image-file-types"></a>Bilddateitypen  
 Die folgenden Bilddateitypen können verwendet werden, um den standardmäßigen Hintergrund und das Website-Logo zu ersetzen:  
  
-   Bitmap (*. BMP, \*. DIB, \*. RLE)  
  
-   GIF (*.gif)  
  
-   PNG (*.png)  
  
-   JPG (*.jpg)  
  
###  <a name="BKMK_RepairRWA"></a>Remote Webzugriff reparieren  
 Der Reparaturassistent unterstützt Sie beim Erkennen und Beheben von Problemen mit dem Router oder dem Domänennamen. Es gibt zwei Möglichkeiten zum Ermitteln von Problemen mit dem Remotewebzugriff:  
  
-   In den Servereinstellungen im Dashboard wird auf der Registerkarte "Zugriff überall" ein Symbol mit einem roten X zusammen mit einer Beschreibung des Problems angezeigt.  
  
-   Eine Warnung in der Meldungsanzeige.  
  
> [!NOTE]
>  Der Reparaturassistent ist nicht verfügbar, bis Sie den Remotewebzugriff wieder aktivieren. Weitere Informationen zum Aktivieren des Remotewebzugriffs finden Sie unter [Aktivieren des Remotewebzugriffs](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_TurnOnRWA).  
  
##### <a name="to-repair-remote-web-access"></a>So reparieren Sie den Remotewebzugriff  
  
1.  Melden Sie sich beim Dashboard an.  
  
2.  Klicken Sie auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
3.  Klicken Sie auf **Reparatur**. Die Assistent zum **Reparieren des Remotewebzugriffs** wird gestartet.  
  
4.  Klicken Sie auf **Weiter**. Der Assistent analysiert den Remotewebzugriff, identifiziert das Problem und versucht anschließend, das Problem zu beheben.  
  
5.  Wenn nach Beenden des Assistenten eine Warnung angezeigt wird, können Sie auf **Wiederholung** klicken, um zu versuchen, das Problem erneut zu reparieren. Wenn Sie weiterhin eine Warnung erhalten, überprüfen Sie die Warnung auf weitere Informationen zu dem Problem und auf Schritte zur Problembehandlung.  
  
##  <a name="BKMK_5"></a>Problembehandlung bei Remote Webzugriff  
  
-   [Behandeln von Problemen mit der Remote Webzugriff Konnektivität](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [Behandeln von Problemen mit der Firewall](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  
  
-   [Problembehandlung bei "Zugriff überall"](../support/Troubleshoot-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Remote Desktop Optionen](Remote-desktop-options.md)  
  
-   [Remote Webzugriff verwenden](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Zugriff überall verwalten](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
