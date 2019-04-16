---
title: Verwalten von Office365 in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
0author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b45bddb657b96c7cc5f9291a6c887b9d0801974b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Verwalten von Office365 in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Wenn Sie Ihre Windows Server Essentials-Server mit Microsoft Office365 integrieren, können Sie Ihre Office365-Dienste und Onlinekonten zusammen mit den lokalen Ressourcen über das Windows Server Essentials-Dashboard verwalten. In diesem Thema erfahren Sie alles Sie, welche Vorteile Sie durch die Integration von Ihrem Servers mit Office365, wie folgt vor, und die Verwaltung und Problembehandlung bei der Integration von Office365.  
  
  
  
> [!IMPORTANT]
>   Office365-Integration ist nur in Umgebungen mit einem einzelnen Domänencontroller unterstützt. Darüber hinaus muss die Office365-Integrations-Assistent auf einem Domänencontroller ausführen.  
  
## <a name="in-this-topic"></a>In diesem Thema  
  
-   [Warum sollte ich Office365 in den Server integrieren?](#BKMK_IntegrationOverview)  
  
-   [Einrichten der Office365-Integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Verwalten von Office365-Integration](#BKMK_ManageIntegration)  
  
-   [Problembehandlung bei Office365-Integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a>Warum sollte ich Office365 in den Server integrieren?  
 Es gibt viele gute Gründe für Office365 in Ihren Windows Server Essentials-Server zu integrieren. Wenn Sie einige Ihrer Ressourcen intern verwalten, aber Office365 für andere Dienste verwenden, Sie alles möglicherweise beim Verwalten von Office365-Dienste und Ressourcen über das Dashboard, zusammen mit lokalen Ressourcen, statt an zwei Orten zu arbeiten.  
  
-   Verwalten Sie Onlinekonten, mit denen den Benutzerzugriff auf Office365 zusammen mit Ihren Benutzerkonten:  
  
    -   Erstellen von Microsoft Online Services-Konten für die Benutzer in einem einzigen Schritt, oder erstellen Sie Benutzerkonten auf dem Server für Ihren vorhandenen Onlinekonten. Sie können auch ein Onlinekonto zu einem neuen oder vorhandenen Benutzerkonto hinzufügen.  
  
         Bei der Erstellung der Onlinekonten über das Dashboard melden Sie sich Benutzer Office365 mit demselben Kennwort an, die, das Sie auf dem Server zu verwenden. Wenn sie das Kennwort für dieses Benutzerkonto ändern, ändert sich der Online-Kennwort auch. Und Sie wissen, dass die Kennwörter der Onlinekonten immer die Sicherheitsanforderungen erfüllen, die Sie für Ihre Benutzerkonten festlegen.  
  
    -   Verwalten Sie Onlinekonten zusammen mit dem Benutzerkonto während des Lebenszyklus des Benutzerkontos. Wenn Sie ein Benutzerkonto deaktivieren, wird das Onlinekonto ebenfalls deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt.  
  
    -   Verwalten von Exchange Online-Verteilergruppen für E-Mails auch auf einem Windows Server Essentials-Server.  
  
-   Senden und Empfangen von E-Mails von Ihrem Unternehmen s Internetdomäne (z.B. contoso.com) durch eine benutzerdefinierte Internetdomäne mit Ihrem Office365-Abonnement verknüpft.  
  
-   Verwalten des Abonnements und Office365-Integration über das Dashboard.  
  
-   Wenn Ihr Abonnement SharePoint Online-Bibliotheken enthält, können Sie Office365-Integration mit einem Windows Server Essentials-Server:  
  
    -   Erstellen und Verwalten von SharePoint Online-Bibliotheken über das Dashboard.  
  
        > [!NOTE]
        >  Alles Sie möglicherweise auch die My Server2012 R2-App verwenden, um mit Dokumenten in SharePoint Online-Bibliotheken über Ihr Laptop, Mobilgerät oder Windows Phone zu arbeiten. Dieses Feature ist nur verfügbar für Windows Server Essentials. Weitere Informationen finden Sie unter [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).  
  
    -   Ändern von Berechtigungen für eine SharePoint Online-Team-Website über das Dashboard, oder öffnen Sie die Teamwebsite über das Dashboard, um andere Änderungen vorzunehmen.  
  
     Weitere Informationen finden Sie unter [Verwalten von SharePoint Online](Manage-SharePoint-Online-in-Windows-Server-Essentials.md).  
  
-   Wenn Sie Exchange Online abonnieren, können Sie mithilfe von Office365-Integration mit einem Windows Server Essentials-Server auf die mobilen Geräte verwalten, mit denen die Benutzer mit der E-Mail-Server Ihres Unternehmens herstellen:  
  
    -   Fordern Sie Kennwortschutz, beim E-Mail-Server des Unternehmens mobile Geräten herstellen. Legen Sie eine minimale Kennwortlänge, die Anzahl der fehlgeschlagenen Anmeldeversuche zu ermöglichen und die minimal erforderliche Zeit zwischen Anmeldeversuchen.  
  
    -   Blockieren Sie ein mobiles Gerät eine Verbindung zu Exchange Online herstellen, wenn Ihnen Sicherheitsprobleme mit dem Modell bekannt.  
  
    -   Wenn ein mobiles Gerät verloren geht oder gestohlen wird, löschen Sie das Gerät, um sensible Daten beim nächsten löschen, die das Gerät eingeschaltet ist.  
  
-    Office365-Integration bietet Ihnen neue Möglichkeiten zur Verbindung mit Office365-Dienste und Ressourcen:  
  
    -   Öffnen Sie Office365-Dienste von Windows Server Essentials-Launchpad. Weitere Informationen finden Sie unter [Quick Start Guide to Using Microsoft Office365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).  
  
    -   Verwenden Sie die My Server2012 R2-App, um mit Dokumenten in SharePoint Online-Bibliotheken über Ihr Laptop, Mobilgerät oder Windows Phone zu arbeiten. Weitere Informationen finden Sie unter [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md). Dieses Feature ist nur verfügbar in Windows Server Essentials.  
  
##  <a name="BKMK_Configure"></a>Einrichten der Office365-Integration  
 Sie können den Server mit Office365 integrieren, jederzeit nach Abschluss der Serverinstallation. Wenn Sie t nicht bereits über ein Office365-Abonnement verfügen, können Sie eines erwerben oder für ein kostenloses Testabonnement anmelden.  
  
 Sie können die folgenden Aufgaben ausführen:  
  
-   [Schritt1: Überprüfen der integrationsvoraussetzungen für Office365](#BKMK_StepOne_VERIFY)  
  
-   [Schritt2: Integrieren des Servers mit Microsoft Office365](#BKMK_StepTwo)  
  
-   [Schritt3: Verknüpfen Sie Ihrer Organisation s Internetdomänennamens mit Office365 (optional)](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a>Schritt1: Überprüfen der integrationsvoraussetzungen für Office365  
 Bevor Sie beginnen, stellen Sie sicher, dass der Server diese Anforderungen erfüllt:  
  
-   Der Server kann eines dieser Betriebssysteme verfügen: Windows Server Essentials, Windows Server Essentials oder dem Betriebssystem Windows Server2012 R2 Standard oder Windows Server2012 R2 Datacenter mit installierter Windows Server Essentials Experience-Rolle.  
  
-   Die Umgebung kann nur einen Domänencontroller haben, und Sie müssen Office365-Integration auf dem Domänencontroller durchführen.  
  
-   Sie müssen auf dem Server mit dem Internet herstellen können.  
  
-   Sie sollten alle wichtigen Updates auf dem Server installieren, bevor Sie Office365-Integration starten.  
  
-   Wenn Sie die s Internetdomäne Ihrer Organisation in E-Mail-Adressen und mit den SharePoint Online-Ressourcen verwenden möchten, müssen Sie alles den Domänennamen registrieren, damit Sie die Domäne mit Office365 während der Integration verknüpfen können. Weitere Informationen finden Sie unter [zum Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).  
  
> [!NOTE]
>  Sie Verschlüsselungskennwort ist nicht erforderlich, im Voraus zu Office365 zu abonnieren. Sie alles in der Lage, ein Abonnement erwerben oder registrieren Sie sich für eine kostenlose Testversion während der Integration von Office365. Wenn Sie d Pläne und Preise für Office365 ansehen möchten [Vergleichen von Office365-Pläne für Unternehmen](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text).  
  
###  <a name="BKMK_StepTwo"></a>Schritt2: Integrieren des Servers mit Microsoft Office365  
 Führen Sie das folgende Verfahren auf dem Domänencontroller, auf den Windows Server Essentials-Server mit Office365 integrieren.  
  
> [!NOTE]
>  Das Verfahren s gleich, ob Sie Windows Server Essentials oder Windows Server Essentials, aber Sie alles von einem anderen Ort auf der Startseite gestartet haben. In Windows Server Essentials integrieren Sie den Server mit Office365 und anderen Microsoft Online Services auf die **Dienste** Registerkarte. Integration von Office365 erfolgt in Windows Server Essentials auf den **E-Mail** Registerkarte.  
  
##### <a name="to-integrate-the-server-with-office-365"></a>Der Server mit Office365 integrieren  
  
1.  Melden Sie sich auf dem Server als Administrator, und öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Auf der **Home** auf **Dienste** (in Windows Server Essentials, klicken Sie auf **E-Mail**), klicken Sie auf **in Microsoft Office365 integrieren**, und klicken Sie dann auf **Microsoft Office365-Integration einrichten**.  
  
     Die Integration mit Microsoft Office365-Assistent wird angezeigt.  
  
3.  Auf der **Einstieg in die** Seite, eine der folgenden Aktionen:  
  
    -   Wenn Sie vergessen ein Office365-Abonnement verfügen, klicken Sie auf **Weiter**, und folgen Sie die Anweisungen, um Office365 oder melden Sie für ein Testabonnement abonnieren.  
  
         Sie müssen sich bei Office365 anmelden, bevor Sie zum Assistenten zurückkehren. Aber Sie Verschlüsselungskennwort ist nicht erforderlich, führen Sie die Aufgaben in der **beginnen Sie hier** Abschnittder Office365-Portal.  
  
    -   Wenn Sie bereits über ein Office365-Abonnement verfügen, die Sie mit dem Server, wählen Sie integrieren möchten **ich habe bereits ein Abonnement für Office365**, und klicken Sie dann auf **Weiter**.  
  
4.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
 Nach dem erfolgreichen Abschluss des Assistenten Sie alles Beachten Sie die folgenden Änderungen am Dashboard:  
  
-   Dort s ein neues **Office365** Seite, die verwendet wird, um die Integration und Office365-Abonnement zu verwalten.  
  
-   Auf der **Benutzer** Seite, die Sie alles finden Sie unter einer **Onlinekonten** Registerkarte können Sie erstellen und verwalten die Microsoft Online Services-Konten, die die Benutzer Zugriff auf Office365 zu ermöglichen. Wenn Sie mit Online austauschen und verfügen über einen Windows Server Essentials-Server, Sie auch angezeigt, eine **Verteilergruppen** Registerkarte.  
  
-   Die **Speicher** Seite auf einem Windows Server Essentials-Server verfügt über eine **SharePoint-Bibliotheken** Registerkarte zum Verwalten von SharePoint Online-Bibliotheken und Ändern von Berechtigungen für Teamwebsites. Jeder Geschäftsplan für Office 365 enthält diese grundlegenden SharePoint Online-Features.  
  
###  <a name="BKMK_StepThree"></a>Schritt 3: Verknüpfen Sie Ihrer Organisation s Internetdomänennamens mit Office 365 (optional)  
 Wenn Sie Ihre eigene Internetdomäne in e-Mails mit Ihrer Organisation und die URLs für Ihre SharePoint Online-Ressourcen verwenden möchten, können Sie eine benutzerdefinierte Domäne mit Office 365-Abonnement verknüpfen. Wenn Sie Ihre Windows Server Essentials-Server mit Office 365 integrieren, können Sie das Dashboard dazu.  
  
 Es am einfachsten, dies tun, bevor Sie online erstellen s Konten für Ihre Benutzer damit Sie die Domäne verwenden können, wenn Sie per Massenimport die Onlinekonten erstellen.  
  
 Wenn Sie Office365 registrieren, erhalten Sie einen Domänennamen? z.B. *Contoso*. onmicrosoft.com. Wenn Sie d lieber einen anderen Domänennamen verwenden? sagen Sie einfach contoso.com? Sie können. Sie müssen sich die erwerben eines Domänennamens Wenn Sie t nicht bereits eigene und einige DNS-Einträge ändern.  
  
 Einrichten einer benutzerdefinierten Domäne mit Office 365 umfasst vier Aufgaben:  
  
1.  **Erwerben eines Domänennamens.** Das heißt, registrieren Sie ihn mit einer domänenregistrierungsstelle oder DNS-Hostinganbieter.  
  
    -   Wählen Sie einen Domänennamen, der mit Office 365 verwendet werden kann. Können Sie einen Namen für die Domäne der Ebene 2? z.B. buycontoso.com? jedoch keine Ebene 3 Domänennamen? z.B. Marketing.contoso.com. Weitere Informationen zum Auswählen einer Domäne in Office365 verwenden, finden Sie unter [Domänen](https://technet.microsoft.com/library/office-365-domains.aspx).  
  
    -   Kaufen sie über einer domänenregistrierungsstelle, die die Domänennamenserver (DNS)-Einträge erforderlichen Office 365 ermöglicht. Um herauszufinden, welche domänenregistrierungsstellen die erforderlichen DNS-Einträge ermöglichen, finden Sie unter [zum Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660). Wenn Sie Ihre Domäne bereits mit einer anderen Registrierungsstelle registriert, Verschlüsselungskennwort Angst; Sie können die Domäne zu einer anderen Registrierungsstelle übertragen, wenn Sie die Domäne mit Office 365 verknüpfen.  
  
2.  **Konfigurieren Sie DNS-Einträge, die Office 365-Dienste verwenden Sie den Domänennamen zu ermöglichen.** Die einfachste Möglichkeit ist, damit der Assistent die DNS-Einträge für Sie konfigurieren, wenn Sie die Domäne mit Office 365-Abonnement in Schritt 3 verknüpfen. Wenn Sie d dies stattdessen selbst vornehmen, finden Sie unter [Gewusst wie: Manuelles Konfigurieren von DNS-Einträgen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS).  
  
3.  **Verknüpfen Sie Ihre benutzerdefinierte Internetdomäne mit Ihrem Office 365-Abonnement.** Alles verwenden Sie die **Domäne mit Office 365 verknüpfen** Aktion.  
  
4.  **Stellen Sie sicher, dass Ihre Office 365-Dienste den neuen Domänennamen verwenden.**  
  
 Wenn Sie die Schritte 1 und 2 abschließen, bevor Sie verwenden die **Domäne mit Office 365 verknüpfen** Aufgabe der Assistent den Domänennamen mit Office 365 verknüpfen kann. Alternativ können Sie der Assistent mit einigen oder allen Schritten 1 und 2 unterstützen.  
  
##### <a name="to-link-your-organization-s-internet-domain-to-office-365"></a>So verknüpfen Sie die Internetdomäne Ihrer Organisation s mit Office 365  
  
1.  Öffnen Sie auf dem Dashboard die **Office 365** Seite, und klicken Sie auf **Domäne mit Office 365 verknüpfen**.  
  
2.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
     Der Assistent hilft Ihnen mit einigen oder allen Schritten zum Registrieren, konfigurieren und Verknüpfen einer neuen oder vorhandenen Internetdomänennamens in Office 365 verwenden.  
  
     Klicken Sie auf den Hilfelink auf der Seite des Assistenten, um die Informationen abzurufen, die Sie benötigen, um einen Vorgang abzuschließen. Oder Lesen Sie die Einrichtung einer Domäne Namenabschnitt [Manage Remote Web Access in Windows Server Essentials](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) für eine Prozessübersicht und Anforderungen.  
  
    > [!NOTE]
    >  Um den Assistenten verwenden, um einen neuen Domänennamen zu registrieren, müssen Sie eine der Domain Name Service-Anbieter verwenden, die mit Microsoft, um eine nahtlose Integration mit dem Assistenten bereitstellen zu können. Eine Domänennamen-Registrierungsstelle finden Sie unter [zum Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).  
  
3.  Wenn der Assistent erkennt, dass Ihre Domäne Name nicht vom Server verwaltet, müssen Sie alles zum Abschließen der Konfiguration der erforderlichen DNS-Einträge manuell konfigurieren. Anweisungen finden Sie unter [Gewusst wie: Manuelles Konfigurieren von DNS-Einträgen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS)weiter unten in diesem Thema.  
  
4.  Stellen Sie sicher, dass die Domäne in Office 365 verwendet wird.  
  
     Dort s eine kurze Wartezeit nach Abschluss des Assistenten während der Domänennamen-Registrierungsstelle die DNS-Einträge überprüft. Dies geschieht automatisch. Vergessen Sie nichts zu tun haben. Aber es in der Regel dauert etwa eine Stunde? und manchmal etwas länger. Nach Abschluss der Überprüfung der Domäne der **Office 365** Seite Ihrer Organisation s Domäne aufgelistet.  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a>So konfigurieren Sie DNS-Einträge für Office 365-integration  
 Wenn die Verknüpfung Ihrer Domäne zu Office 365-Assistenten erkennt, dass der Domänenname nicht vom Server verwaltet wird, müssen zum Abschließen der Konfiguration Sie manuell die erforderlichen Domänennamenserver (DNS)-Einträge konfigurieren. In diesem Fall finden Sie alles eine Liste der DNS-Einträge, die Sie konfigurieren müssen **%username%\NewDNSRecords_ (n) .txt**, wobei *(n)* eine zufällige Zahl ist.  
  
 Die folgende Tabelle beschreibt die DNS-Einträge, die Sie hinzufügen müssen. Eintragsmethoden können bei unterschiedlichen Domänennamen-Registrierungsstellen variieren. Wenn Sie Fragen haben, erhalten Sie die Domänennamen-Registrierungsstelle.  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>DNS-Einträge für die Verknüpfung eines benutzerdefinierten Internetdomänennamens mit Office 365  
  
|Dienst|Erforderliche DNS-Einträge|Zweck|  
|-------------|--------------------------|-------------|  
|(Mehrere Dienste)|MX| Office 365 verwendet dieser Eintrag, um sicherzustellen, dass Sie einen bestimmten Domänennamen besitzen. Dieser MX-Eintrag nicht für das routing von e-Mail-Nachrichten stören.|  
|Exchange Online|MX|Enthält das routing von e-Mail-Nachrichten. **Wichtig:** Wenn Sie e-Mails migrieren können, weisen Sie keine Einstellung Null (**0**) an den neuen MX-Datensatz. Stellen Sie sicher, dass der Wert für den Eintrag größer als der Wert ist, die den aktuellen MX-Eintrag zugewiesen ist. Wenn die e-Mail-Migration abgeschlossen ist, und Sie bereit sind, ändern Sie den e-Mail-Server zu Office 365, können Sie die Domänennamen-Registrierungsstelle den Präferenzwert des neuen MX-Eintrags zurückgesetzt.|  
|Exchange Online|Alias (CNAME)|AutoErmittlungs-Eintrag, der verwendet wird, damit Benutzer einfach richten Sie eine Verbindung zwischen Exchange Online und ihre Outlook-desktop-Client oder einem mobilen e-Mail-Client. **Hinweis:** , wenn Sie Outlook Web Access mithilfe Ihrer eigenen Organisation s Domänennamen (z. B. http://mail.contoso.com) statt der standard-URL (https://outlook.com/owa/office365.com) zugreifen möchten, können Sie den Aliaseintrag (CName) wie folgt konfigurieren: **Typ CNAME TTL = = 01: 00:00, HostName = Mail Address=mail.office365.com**|  
|Exchange Online|TXT|Gibt an, dass diese die Domäne outlook.com, indem Sie die Office 365-e-Mail-Server verwendet zum Senden von e-Mails für Ihre Domäne autorisiert ist. Erstellen Sie diesen Eintrag, um zu verhindern, dass Ihre ausgehenden e-Mail-Adresse, die als Spam gekennzeichnet werden.|  
|Lync Online|SRV|Hilft, Verbund mit anderen instant messaging-Diensten wie Windows Live oder Yahoo! zu ermöglichen.|  
|Lync Online|SRV|AutoErmittlungs-Eintrag, der verwendet wird, damit Benutzer einfach richten Sie eine Verbindung zwischen dem Lync-Desktopclient und Microsoft Lync Online.|  
  
> [!IMPORTANT]
>  Nach der Domäne Überprüfung abgeschlossen ist, versuchen Sie nicht, hinzufügen oder keine weiteren Änderungen an die DNS-Einträge aus dem Office 365-Portal.  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a>Als Nächstes  
  
-   Microsoft Online Services-Konten für die Benutzer zu erstellen.  
  
     Um Office 365-Dienste zu verwenden, müssen die Benutzer ein Microsoft Online Services-Konto, das deren Netzwerkbenutzerkonto zugeordnet haben. Dies wird durch das Dashboard erleichtert. Wenn Sie ein neues Office 365-Abonnement verwenden, Sie per Massenimport-Onlinekonten für vorhandene Benutzerkonten erstellen können. Wenn Sie einen neuen Server Integration von Office 365-Abonnement, dass Sie bereits verwenden, Benutzerkonten importiert werden können von der vorhandenen online Konten. Informationen zu entsprechenden Verfahren finden Sie unter [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
> [!NOTE]
>  Microsoft Online Services-Konten werden auf dem Dashboard in Windows Server Essentials als Office 365-Konten bezeichnet. Die Konten sind identisch. nur die Terminologie geändert.  
  
##  <a name="BKMK_ManageIntegration"></a>Verwalten von Office 365-integration  
 Nachdem Sie den Server mit Office 365 Integrieren der **Office 365** -Seite des Dashboards zeigt Informationen zu Office 365-Abonnement und stellt diese Aufgaben zur Verfügung:  
  
-   [Verwalten von Office 365-Abonnement](#BKMK_ManageO365) ? Ändern Sie das Administratorkonto, das Sie verwenden, um das Abonnement zu verwalten. Öffnen Sie die Office 365-Administratordashboard, um das Abonnement zu verwalten.  
  
-   [Verknüpfen der Internetdomäne Ihrer Organisation s mit Office 365](#BKMK_StepThree) ? Wenn Sie senden und Empfangen von e-Mails mit Ihrer eigenen Domäne möglich sein soll, können Sie die Domäne mit Office 365 verknüpfen. (Zuvor erläutert in [Schritt 3: Verknüpfen Sie Ihre Organisation s-Domäne mit Office 365](#BKMK_StepThree).)  
  
-   [Deaktivieren der Integration von Office 365](#BKMK_Disable) ? Wenn Sie vergessen des Office 365-Dienste, Abonnements und online-Konten über das Dashboard verwalten möchten, können Sie Office 365-Integration deaktivieren. Die Dienste sind weiterhin verfügbar, auf dem Office 365-Portal.  
  
###  <a name="BKMK_ManageO365"></a>Verwalten von Office 365-Abonnement  
 Wenn Sie Office 365-Abonnement während Sie arbeiten, auf dem Server ändern möchten, öffnen Sie das Abonnement in Office 365 aus den **Office 365** -Seite des Dashboards. Sie können auch das Administratorkonto ändern, die vom Server, Office 365-Dienste zu ändern.  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Öffnen Sie das Abonnement mit dem Office 365-Administratordashboard  
  
1.  Öffnen Sie auf dem Windows Server Essentials-Dashboard die **Office 365** Seite.  
  
2.  In **Konfigurationsaufgaben**, klicken Sie auf **Verwalten von Office 365**.  
  
3.  Melden Sie sich bei Office 365 mit Microsoft-Onlinekonto, mit denen Sie das Abonnement zu verwalten.  
  
     Office 365-Administratordashboard wird geöffnet.  
  
##### <a name="to-change-the-office-365-administrator-account"></a>So ändern Sie das Office 365-Administratorkonto  
  
1.  Klicken Sie auf dem Dashboard auf **Office 365**.  
  
2.  In **Konfigurationsaufgaben**, klicken Sie auf **ändern Sie das Office 365-Administratorkonto**. Der Assistent zum Ändern des Administrator-Konto angezeigt wird. (In Windows Server Essentials, wird der Assistent die Office 365-Administratorkonto einrichten bezeichnet.)  
  
3.  Geben Sie die Anmeldeinformationen für das Konto, das Sie zum Verbinden mit Office 365-Abonnement, und klicken Sie dann auf verwenden möchten **Weiter**.  
  
4.  Klicken Sie auf **schließen **. Das Dashboard wird neu gestartet.  
  
###  <a name="BKMK_Disable"></a>Deaktivieren der Integration von Office 365  
 Wenn Sie sich entscheiden, dass Sie keine Nachteile für Ihr Ihre Office 365-Dienste und online-Konten über das Dashboard verwalten möchten, können Sie Office 365-Integration deaktivieren. Office 365-Abonnement bleibt aktiv und über das Dashboard vorgenommenen konfigurationsänderungen bleiben bestehen. Z. B. erhalten Sie alle e-Mails an einen Domänennamen, den mit Ihrem Office 365-Abonnement verknüpft. Sie gewonnen keine e-Mails verloren gehen, und Steuerelemente, die Sie für mobile Geräte festgelegt sind immer noch Exchange Online verwendet.  
  
 In Zukunft Sie Ihre Office 365-Abonnement, Dienste und Ressourcen in Office 365 verwalten, und die Benutzer müssen die Kennwörter für ihre online-Konten in Office 365 verwalten. Kennwortsynchronisierung erfolgt nicht mehr, und deaktivieren oder Entfernen eines Benutzerkontos hat keine Auswirkung auf das Benutzerkonto s online an.  
  
 Da die Office 365-Integrationssoftware auf dem lokalen Server installiert ist, können Sie das Feature deaktivieren, auch wenn der Integrationsdienst keine Verbindung mit Office 365 herstellen kann.  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>So deaktivieren Sie Office 365-Integration mit dem server  
  
1.  Klicken Sie auf dem Dashboard auf **Office 365**.  
  
2.  Klicken Sie auf **Deaktivieren der Integration von Office 365**. Der Assistent Deaktivieren von Office 365 wird angezeigt.  
  
3.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
> [!NOTE]
>  Um Office 365-Integration erneut zu aktivieren, verwenden die **in Office 365 integrieren** Aufgabe auf den **Service** Registerkarte im Dashboard s **Home** Seite. Anweisungen finden Sie unter [Schritt2: Integrieren des Windows Server Essentials-Servers mit Microsoft Office 365](#BKMK_StepTwo)weiter oben in diesem Thema.  
  
##  <a name="BKMK_Troubleshoot"></a>Problembehandlung bei Office 365-integration  
 Dieser Abschnitt enthält Informationen, damit Sie häufige Probleme beheben, die auftreten können, wenn das Office 365-Integration in Windows Server Essentials verwenden.  
  
###  <a name="BKMK_AcctsNotCreated"></a>Einige Microsoft Online Services-Konten wurden nicht erstellt.  
 **Beschreibung**  
  
 Der Versuch, ein oder mehrere Microsoft Online Services-Konten aus der Dashboard-t war nicht erfolgreich erstellen.  
  
 **Lösung**  
  
1.  Klicken Sie auf die Abschlussseite des Assistenten, um eine Ergebnisdatei zu öffnen, die detaillierte Informationen zu jeder Anforderung zum Erstellen eines Kontos enthält, die nicht erfolgreich abgeschlossen wurde. Beispielsweise kann ein Ergebnis Ihnen aufzeigen, dass ein Microsoft Online Services-Konto mit dem Namen eines angeforderten Kontos bereits vorhanden ist.  
  
2.  Führen Sie die empfohlenen Aktionen auf jeden Fehler zu beheben.  
  
3.  Wenn dieses Problem weiterhin auftritt, starten Sie den Server neu, und wiederholen Sie die Onlinekonten erneut zu erstellen.  
  
###  <a name="BKMK_ProblemUninstalling"></a>Es liegt ein Problem mit dem Deinstallieren von Office 365-Integration  
 **Beschreibung**  
  
 Fehler bei dem Versuch der Integration von Office 365 zu deaktivieren.  
  
 **Lösung**  
  
1.  Stellen Sie sicher, dass der Computer mit dem Internet verbunden ist, und versuchen Sie es dann erneut.  
  
2.  Wenn der Fehler erneut auftritt, starten Sie den Server neu, und versuchen Sie es dann erneut.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Services Integration Overview for Windows Server Essentials - Teil 1](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Services Integration Overview for Windows Server Essentials - Teil 2](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Erste Schritte für die Verwendung von Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)
