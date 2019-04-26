---
title: Verwalten von Office 365 in Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860501"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Verwalten von Office 365 in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Ihre Windows Server Essentials-Server mit Microsoft Office 365 integrieren, können Sie Ihre Office 365-Dienste und Onlinekonten zusammen mit lokalen Ressourcen aus dem Windows Server Essentials-Dashboard verwalten. In diesem Thema erfahren Sie ll Sie, welche Vorteile Sie durch die Integration Ihres Servers mit Office 365, wie es geht und wie Sie die Verwaltung und Problembehandlung Ihrer Office 365-Integration.  
  
  
  
> [!IMPORTANT]
>   Office 365-Integration wird nur in Umgebungen mit einem einzelnen Domänencontroller unterstützt. Darüber hinaus muss den Assistenten zum Office 365-Integration auf einem Domänencontroller ausführen.  
  
## <a name="in-this-topic"></a>Inhalt dieses Themas  
  
-   [Warum sollte ich Office 365 in den Server integrieren?](#BKMK_IntegrationOverview)  
  
-   [Einrichten der Office 365-integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Verwalten von Office 365-integration](#BKMK_ManageIntegration)  
  
-   [Problembehandlung bei Office 365-integration](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a> Warum sollte ich Office 365 in den Server integrieren?  
 Es gibt viele gute Gründe für Office 365 in Ihren Windows Server Essentials-Server zu integrieren. Wenn Sie einige Ihrer Ressourcen intern verwalten, aber Office 365 für andere Dienste verwenden, werden Sie ll verwalten Sie Ihre Office 365-Dienste und Ressourcen über das Dashboard zusammen mit lokalen Ressourcen, statt an zwei Orten zu arbeiten.  
  
-   Verwalten Sie Onlinekonten, mit denen Ihre Benutzerzugriff auf Office 365 zusammen mit Ihren Benutzerkonten:  
  
    -   Erstellen Sie Microsoft Online Services-Konten für die Benutzer in einem einzigen Schritt, oder erstellen Sie Benutzerkonten auf dem Server für bereits vorhandene Onlinekonten. Sie können auch ein Onlinekonto zu einem neuen oder bereits vorhandenen Benutzerkonto hinzufügen.  
  
         Bei der Erstellung der Onlinekonten über das Dashboard melden Benutzer Office 365 mit dem gleichen Kennwort an, die, das Sie auf dem Server zu verwenden. Wenn sie das Kennwort für dieses Benutzerkonto ändern, ändert sich auch das Online-Kennwort. Und Sie können sich sicher sein, dass die Kennwörter der Onlinekonten immer die Sicherheitsanforderungen erfüllen, die Sie für Ihre Benutzerkonten festlegen.  
  
    -   Verwalten Sie Onlinekonten zusammen mit Benutzerkonten, während des gesamten Lebenszyklus der Benutzerkonten. Wenn Sie ein Benutzerkonto deaktivieren, wird auch das Onlinekonto deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt.  
  
    -   Verwalten Sie auf einem Windows Server Essentials-Server Exchange Online-Verteilergruppen für e-Mails auch ein.  
  
-   Senden und Empfangen von e-Mail-Adresse aus der Internetdomäne Ihrer Organisation-s (beispielsweise "contoso.com") durch eine benutzerdefinierte Internetdomäne mit Ihrem Office 365-Abonnement verknüpfen.  
  
-   Verwalten Sie Ihr Abonnement und die Integration von Office 365 über das Dashboard an.  
  
-   Wenn Ihr Abonnement SharePoint Online-Bibliotheken umfasst, können Sie Office 365-Integration mit einem Windows Server Essentials-Server:  
  
    -   Erstellen und Verwalten von SharePoint Online-Bibliotheken über das Dashboard.  
  
        > [!NOTE]
        >  Sie alle möglicherweise auch die My Server 2012 R2-app zum Arbeiten mit Dokumenten in SharePoint Online-Bibliotheken über Ihr Laptop, Mobilgerät oder Windows Phone verwenden. Dieses Feature steht nur für Windows Server Essentials. Weitere Informationen finden Sie unter [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).  
  
    -   Ändern Sie der Berechtigungen für eine SharePoint Online-Teamwebsite über das Dashboard, oder öffnen Sie die Teamwebsite über das Dashboard, um andere Änderungen vorzunehmen.  
  
     Weitere Informationen finden Sie unter [Verwalten von SharePoint Online](Manage-SharePoint-Online-in-Windows-Server-Essentials.md).  
  
-   Wenn Sie Exchange Online abonnieren, kann Office 365-Integration mit einem Windows Server Essentials-Server die mobilen Geräte zu verwalten, die Ihre Benutzer für die Verbindung mit Ihrer Unternehmens-e-Mail-Server verwenden:  
  
    -   Fordern Sie Kennwortschutz, wenn sich mobile Geräte mit dem E-Mail-Server des Unternehmens verbinden. Legen Sie eine minimale Kennwortlänge, die Anzahl der zulässigen fehlgeschlagenen Anmeldeversuche und die minimal erforderliche Zeit zwischen Anmeldeversuchen fest.  
  
    -   Blockieren Sie ein mobiles Gerät, das eine Verbindung zu Exchange Online herstellen möchte, wenn Ihnen Sicherheitsprobleme mit dem Modell bekannt sind.  
  
    -   Wenn ein mobiles Gerät verloren geht oder gestohlen wird, löschen Sie das Gerät, um sensible Daten zu löschen, wenn das Gerät das nächste Mal aktiviert wird.  
  
-    Office 365-Integration bietet Ihnen neue Möglichkeiten für Verbindungen mit Office 365-Dienste und Ressourcen:  
  
    -   Öffnen Sie Office 365-Dienste aus dem Windows Server Essentials-Launchpad an. Weitere Informationen finden Sie unter [Quick Start Guide to Using Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).  
  
    -   Verwenden Sie die My Server 2012 R2-app, um mit Dokumenten in SharePoint Online-Bibliotheken über Ihr Laptop, Mobilgerät oder Windows Phone zu arbeiten. Weitere Informationen finden Sie unter [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md). Dieses Feature steht nur in Windows Server Essentials.  
  
##  <a name="BKMK_Configure"></a> Einrichten der Office 365-integration  
 Sie können den Server mit Office 365 integrieren, zu einem beliebigen Zeitpunkt nach Abschluss die Serverinstallation. Wenn Sie t nicht bereits über ein Office 365-Abonnement verfügen, können Sie erwerben oder registrieren Sie sich für ein kostenloses Testabonnement.  
  
 Führen Sie die folgenden Aufgaben aus:  
  
-   [Schritt 1: Überprüfen der integrationsvoraussetzungen für Office 365](#BKMK_StepOne_VERIFY)  
  
-   [Schritt 2: Integrieren des Servers mit Microsoft Office 365](#BKMK_StepTwo)  
  
-   [Schritt 3: Verknüpfen Sie Ihre Organisation s Internetdomänennamens mit Office 365 (optional)](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a> Schritt 1: Überprüfen der integrationsvoraussetzungen für Office 365  
 Bevor Sie beginnen, stellen Sie sicher, dass der Server die folgenden Anforderungen erfüllt:  
  
-   Der Server kann über diese Betriebssysteme verfügen:  Windows Server Essentials, Windows Server Essentials oder das Betriebssystem Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mit installierter Windows Server Essentials Experience-Rolle.  
  
-   Die Umgebung kann nur einen Domänencontroller haben, und Sie müssen Office 365-Integration auf dem Domänencontroller ausführen.  
  
-   Sie müssen den Server mit dem Internet verbinden können.  
  
-   Vor der Installation von Office 365-Integration, sollten Sie alle kritischen und wichtigen Updates auf dem Server installieren.  
  
-   Wenn Sie die s Internetdomäne Ihrer Organisation in e-Mail-Adressen und Ihre SharePoint Online-Ressourcen verwenden möchten, Sie müssen Sie den Domänennamen registrieren, damit Sie die Domäne mit Office 365 während der Integration verknüpfen können. Weitere Informationen finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).  
  
> [!NOTE]
>  Einbau zusätzlichen t müssen im Voraus zu Office 365 abonnieren. Sie alle möglicherweise-Abonnement erwerben oder registrieren Sie sich für eine kostenlose Testversion während der Integration von Office 365. Wenn Sie d Pläne und Preislisten zu Office 365, ansehen möchten [Vergleich der Office 365-Pläne für Unternehmen](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text).  
  
###  <a name="BKMK_StepTwo"></a> Schritt 2: Integrieren des Servers mit Microsoft Office 365  
 Führen Sie die folgende Schritte auf dem Domänencontroller, um die Integration von Windows Server Essentials-Server in Office 365.  
  
> [!NOTE]
>  Die Prozedur s gleich, ob Sie Windows Server Essentials oder Windows Server Essentials, aber Sie alle von einem anderen Ort auf der Startseite gestartet haben. Unter Windows Server Essentials können Sie den Server mit Office 365 und anderen Microsoft Online Services integrieren, auf die **Services** Registerkarte. In Windows Server Essentials, erfolgt die Integration von Office 365 auf die **-e-Mail** Registerkarte.  
  
##### <a name="to-integrate-the-server-with-office-365"></a>So integrieren Sie den Server mit Office 365  
  
1.  Melden Sie sich auf dem Server als Administrator, und öffnen Sie Windows Server Essentials-Dashboard.  
  
2.  Auf der **Startseite** auf **Services** (Windows Server Essentials, klicken Sie auf **-e-Mail**), klicken Sie auf **in Microsoft Office 365 integrieren**, und klicken Sie dann auf **Microsoft Office 365-Integration einrichten**.  
  
     Der Assistent für die Integration in Microsoft Office 365 wird angezeigt.  
  
3.  Führen Sie auf der Seite **Erste Schritte** eine der folgenden Aktionen aus:  
  
    -   Wenn Sie Ich möchte ein Abonnement für Office 365 verfügen, klicken Sie auf **Weiter**, und befolgen Sie die Anweisungen für Office 365 oder Anmelden einrichten für ein Testabonnement abonnieren.  
  
         Sie müssen für die Anmeldung bei Office 365, bevor Sie zum Assistenten zurückzukehren. Aber Einbau zusätzlichen t muss zum Ausführen der Aufgaben in der **beginnen Sie hier** des Office 365-Portals.  
  
    -   Wenn Sie bereits über ein Office 365-Abonnement, die Sie integrieren möchten verfügen, um mit dem Server, auf **ich besitze bereits ein Abonnement für Office 365**, und klicken Sie dann auf **Weiter**.  
  
4.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
 Nachdem der Assistent erfolgreich abgeschlossen wurde, Sie ll Beachten Sie die folgenden Änderungen an das Dashboard:  
  
-   Dort s ein neues **Office 365** Seite, die zum Verwalten der Integration und Ihr Office 365-Abonnement verwendet wird.  
  
-   Auf der **Benutzer** Page, ll finden Sie eine **Onlinekonten** Registerkarte können Sie erstellen und Verwalten der Microsoft Online Services-Konten, mit denen Ihre Benutzer Zugriff auf Office 365. Wenn Sie erneut mit Online Exchange und verfügen über einen Windows Server Essentials-Server, Sie ll auch finden Sie unter eine **Verteilergruppen** Registerkarte.  
  
-   Die **Storage** Seite auf einem Windows Server Essentials-Server verfügt über eine **SharePoint-Bibliotheken** Registerkarte für die Verwaltung von SharePoint Online-Bibliotheken, und Ändern von Berechtigungen für Teamwebsites. Jeder Geschäftsplan für Office 365 enthält die folgenden grundlegenden SharePoint Online-Features.  
  
###  <a name="BKMK_StepThree"></a> Schritt 3: Verknüpfen Sie Ihre Organisation s Internetdomänennamens mit Office 365 (optional)  
 Wenn Sie Ihre eigene Internetdomäne in e-Mails an Ihre Organisation und die URLs für Ihre SharePoint Online-Ressourcen verwenden möchten, können Sie eine benutzerdefinierte Domäne mit Ihrem Office 365-Abonnement verknüpfen. Wenn Sie Ihre Windows Server Essentials-Server mit Office 365 integrieren, möglich Sie dies über das Dashboard.  
  
 Es s, die am einfachsten, dies tun, bevor Sie online erstellen Konten für Ihre Benutzer, sodass Sie die Domäne verwenden können, wenn Sie per Massenimport die Onlinekonten erstellen.  
  
 Erhalten Sie einen Domänennamen ein, wenn Sie sich für Office 365 registrieren? beispielsweise *Contoso*. onmicrosoft.com. Wenn Sie d stattdessen einen anderen Domänennamen verwenden? z. B. einfach contoso.com? Sie können. Sie müssen zum Erwerben eines Domänennamens Wenn Sie t nicht bereits ein, und einige DNS-Einträge ändern.  
  
 Einrichten einer benutzerdefinierten Domänennamens für die Verwendung mit Office 365 umfasst vier Aufgaben:  
  
1.  **Erwerben eines Domänennamens** Das bedeutet, registrieren Sie ihn über eine Domänenregistrierungsstelle oder einen DNS-Hostinganbieter.  
  
    -   Wählen Sie einen Domänennamen, der mit Office 365 funktioniert. Können Sie einen Namen für die Domäne der Ebene 2.? z. B. buycontoso.com?, jedoch nicht die Namen einer Domäne der Ebene 3.? beispielsweise marketing.contoso.com. Weitere Informationen zum Auswählen einer Domäne in Office 365 verwenden, finden Sie unter [Domänen](https://technet.microsoft.com/library/office-365-domains.aspx).  
  
    -   Kaufen Sie es über einer domänenregistrierungsstelle, die die Domänennamenserver (DNS)-Einträge erforderlich, die von Office 365 ermöglicht. Informationen dazu, welche Domänenregistrierungsstellen die erforderlichen DNS-Einträge ermöglichen, finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660). Wenn Sie bereits Ihre Domäne mit einer anderen Registrierungsstelle registriert haben, Einbau zusätzlichen Sie Sorge; Sie können die Domäne zu einer anderen Registrierungsstelle übertragen, wenn Sie die Domäne mit Office 365 verknüpfen.  
  
2.  **Konfigurieren Sie DNS-Einträge, die Office 365-Diensten ermöglichen, den Domänennamen zu verwenden.** Die einfachste Möglichkeit besteht darin, den Assistenten die DNS-Einträge für Sie konfigurieren, wenn Sie die Domäne in Schritt 3 dem Office 365-Abonnement verknüpfen. Wenn Sie d dies stattdessen selbst vornehmen, finden Sie unter [Vorgehensweise beim manuellen Konfigurieren von DNS-Einträgen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS).  
  
3.  **Verknüpfen Sie Ihre benutzerdefinierte Internetdomäne mit Ihrem Office 365-Abonnement an.** Ll verwenden Sie die **verknüpfen eine Domäne mit Office 365** Aktion.  
  
4.  **Stellen Sie sicher, dass Ihr Office 365-Dienste den neuen Domänennamen verwenden.**  
  
 Wenn Sie die Schritte 1 und 2 abschließen, vor der Verwendung der **verknüpfen eine Domäne mit Office 365** Aufgabe der Assistent kann den Domänennamen mit Office 365 verknüpfen. Alternativ kann Sie der Assistent bei Teilen von oder den gesamten Schritten 1 und 2 unterstützen.  
  
##### <a name="to-link-your-organization-s-internet-domain-to-office-365"></a>So verknüpfen Sie die Internetdomäne Ihrer Organisation s mit Office 365  
  
1.  Öffnen Sie auf dem Dashboard die Seite **Office 365** , und klicken Sie auf **Domäne mit Office 365 verknüpfen**.  
  
2.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
     Des Assistenten können Sie mit einigen oder allen Schritten zum Registrieren, konfigurieren und verknüpfen einen neuen oder vorhandenen Internetdomänennamens für die in Office 365 verwenden.  
  
     Klicken Sie auf den Hilfelink auf der Seite des Assistenten, um die Informationen abzurufen, die Sie benötigen, um eine Aufgabe auszuführen. Oder finden Sie unter den Einrichten einer Domain Name, der Bestandteil [Manage Remote Web Access in Windows Server Essentials](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) für eine Prozessübersicht und Anforderungen.  
  
    > [!NOTE]
    >  Um den Assistenten zu verwenden, um einen neuen Domänennamen zu registrieren, müssen Sie einen Domain Name Service-Anbieter verwenden, der Partner von Microsoft ist, um eine nahtlose Integration mit dem Assistenten bereitstellen zu können. Eine Domänennamen-Registrierungsstelle finden Sie unter [Erwerben eines Domänennamens](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660).  
  
3.  Wenn der Assistent erkennt, dass Ihre Domäne Name ist t vom Server verwaltet werden, Sie müssen die erforderlichen DNS-Einträge zum Abschließen der Konfiguration manuell zu konfigurieren. Anweisungen finden Sie unter [Gewusst wie: Manuelles Konfigurieren von DNS-Datensätzen für die Integration von Office 365](#BKMK_ManuallyConfigureDNS) weiter unten in diesem Thema.  
  
4.  Stellen Sie sicher, dass die Domäne in Office 365 verwendet wird.  
  
     Dort s eine kurze Wartezeit nach dem Abschluss des Assistenten während die Domänennamen-Registrierungsstelle die DNS-Einträge überprüft. Dies geschieht automatisch. Sie Ich möchte müssen nichts weiter tun. Aber in der Regel dauert etwa eine Stunde? und manchmal etwas länger. Bei der Überprüfung der Domäne abgeschlossen ist, wird die **Office 365** -Seite die Domäne Ihrer Organisation s aufgelistet.  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a> Vorgehensweise beim manuellen Konfigurieren von DNS-Einträge für Office 365-integration  
 Wenn der Assistent für die Verknüpfung Ihrer Domäne mit Office 365 erkennt, dass der Domänenname nicht vom Server verwaltet wird, müssen zum Abschließen der Konfiguration manuell die erforderlichen Domänennamenserver (DNS)-Einträge konfigurieren. In diesem Fall Sie finden eine Liste der DNS-Einträge, die Sie konfigurieren müssen **%username%\NewDNSRecords_ (n) .txt**, wobei *(n)* eine zufällige Zahl ist.  
  
 Die folgende Tabelle beschreibt die DNS-Einträge, die Sie hinzufügen müssen. Eintragsmethoden können bei unterschiedlichen Domänennamen-Registrierungsstellen variieren. Wenn Sie Fragen haben, wenden Sie sich an die Domänennamen-Registrierungsstelle.  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>Erforderliche DNS-Einträge für die Verknüpfung eines benutzerdefinierten Internetdomänennamens mit Office 365  
  
|Service|Erforderliche DNS-Einträge|Zweck|  
|-------------|--------------------------|-------------|  
|(Mehrere Dienste)|MX| Office 365 nutzt diesen Eintrag, um sicherzustellen, dass Sie einen bestimmten Domänennamen besitzen. Dieser MX-Eintrag beeinträchtigt das Routing von E-Mail-Nachrichten nicht.|  
|Exchange Online|MX|Ermöglicht Routing von E-Mail-Nachrichten. **Wichtig:**  Wenn Sie E-Mails migrieren, weisen Sie dem neuen MX-Datensatz nicht die Einstellung Null (**0**) zu. Stellen Sie sicher, dass der Wert für den Eintrag größer ist, als der Wert, der dem aktuellen MX-Eintrag zugewiesen ist. Wenn die e-Mail-Migration abgeschlossen ist, und Sie bereit sind, den e-Mail-Server in Office 365 zu ändern, müssen Sie Ihrer Domänennamen-Registrierungsstelle den Präferenzwert des neuen MX-Eintrags zurückgesetzt.|  
|Exchange Online|Alias (CNAME)|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen Exchange Online und dem Outlook-Client auf deren Desktops oder einem mobilen E-Mail-Client zu unterstützen. **Hinweis**:  Wenn Sie Outlook Web access mit Ihren eigenen Domänennamen für die Organisation s möchten (z. B. http://mail.contoso.com) anstelle der standard-URL (https://outlook.com/owa/office365.com), können Sie den Aliaseintrag (CName) wie folgt konfigurieren: **Type=CNAME, TTL=01:00:00, HostName=mail, Address=mail.office365.com**|  
|Exchange Online|TXT|Gibt an, dass diese die Domäne outlook.com, die Office 365-e-Mail-Server ein, die zum Senden von e-Mails für Ihre Domäne autorisiert ist. Erstellen Sie diesen Eintrag, um zu verhindern, dass Ihre ausgehenden E-Mail-Nachrichten als Spam gekennzeichnet werden.|  
|Lync Online|SRV|Hilft, den Verbund mit anderen Instant Messaging-Diensten, wie z. B. Windows Live oder Yahoo! zu ermöglichen.|  
|Lync Online|SRV|AutoErmittlungs-Eintrag, der verwendet wird, um Benutzer beim einfachen Einrichten einer Verbindung zwischen dem Lync-Desktopclient und Microsoft Lync Online zu unterstützen.|  
  
> [!IMPORTANT]
>  Nach Domäne Überprüfung abgeschlossen ist, versuchen Sie nicht zum Hinzufügen oder die DNS-Einträge aus dem Office 365-Portal weitere Änderungen durchführen.  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a> Als Nächstes  
  
-   Erstellen Sie Microsoft Online Services-Konten für die Benutzer.  
  
     Um Office 365-Dienste verwenden zu können, benötigen Ihre Benutzer ein Microsoft Online Services-Konto, das deren Netzwerkbenutzerkonto zugeordnet. Dies ist mit dem Dashboard ganz einfach. Wenn Sie erneut mit der ein neues Office 365-Abonnement, Sie Bulk-Onlinekonten für vorhandene Benutzerkonten erstellen können. Wenn Sie erneut die Integration von einem neuen Server mit Office 365-Abonnement, Sie erneut die bereits mit Benutzerkonten zu importieren, können aus Ihrem vorhandenen online Konten. Anleitungen finden Sie im [Verwalten von Online-Konten für Benutzer](Manage-Online-Accounts-for-Users.md).  
  
> [!NOTE]
>  Microsoft Online Services-Konten werden auf dem Dashboard in Windows Server Essentials als Office 365-Konten bezeichnet. Die Konten sind identisch, nur die Terminologie ist anders.  
  
##  <a name="BKMK_ManageIntegration"></a> Verwalten von Office 365-integration  
 Nachdem Sie Ihre Server mit Office 365 Integrieren der **Office 365** -Seite des Dashboards zeigt Informationen zu Ihrem Office 365-Abonnement, und stellt diese Aufgaben zur Verfügung:  
  
-   [Verwalten Ihres Office 365-Abonnements](#BKMK_ManageO365) ? Ändern Sie das Administratorkonto, mit denen Sie das Abonnement zu verwalten. Öffnen Sie das Office 365-Administratordashboard zum Verwalten Ihres Abonnements.  
  
-   [Verknüpfen der Internetdomäne Ihrer Organisation s mit Office 365](#BKMK_StepThree) ? Wenn zum Senden und Empfangen von e-Mails mit Ihrer eigenen Domäne möglich sein sollen, können Sie die Domäne mit Office 365 verknüpfen. (Zuvor erläutert in [Schritt 3: Verknüpfen Sie Ihre Organisation s-Domäne mit Office 365](#BKMK_StepThree).)  
  
-   [Deaktivieren der Integration von Office 365](#BKMK_Disable) ? Wenn Sie Ich möchte Ihr Office 365-Dienste, Abonnement und -Onlinekonten über das Dashboard verwalten möchten, können Sie Office 365-Integration deaktivieren. Die Dienste sind immer noch auf Office 365-Portal verfügbar.  
  
###  <a name="BKMK_ManageO365"></a> Verwalten Sie Ihres Office 365-Abonnements  
 Wenn Sie Ihre Office 365-Abonnement während Sie erneut das Arbeiten mit dem Server ändern möchten, öffnen Sie das Abonnement in Office 365 aus der **Office 365** Seite des Dashboards. Sie können auch das Administratorkonto ändern, das der Server verwendet, um Office 365-Dienste zu ändern.  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>So öffnen Sie das Abonnement mit dem Office 365-Administratordashboard  
  
1.  Öffnen Sie auf der Windows Server Essentials-Dashboard die **Office 365** Seite.  
  
2.  Klicken Sie unter **Konfigurationsaufgaben**auf **Office 365 verwalten**.  
  
3.  Melden Sie sich für Office 365 mit dem Microsoft online-Konto, mit denen Sie Ihr Abonnement zu verwalten.  
  
     Die Office 365-Administratordashboard wird geöffnet.  
  
##### <a name="to-change-the-office-365-administrator-account"></a>So ändern Sie das Administratorkonto für Office 365  
  
1.  Klicken Sie auf dem Dashboard auf **Office 365**.  
  
2.  Klicken Sie unter **Konfigurationsaufgaben**auf **Office 365-Administratorkonto ändern**. Der Assistent zum Ändern von Administratorenkonten wird angezeigt. (In Windows Server Essentials wird der Assistent die Office 365-Administratorkonto einrichten genannt.)  
  
3.  Geben Sie die Anmeldeinformationen für das Konto, das zum Verbinden mit Ihrem Office 365-Abonnement, und klicken Sie dann auf gewünschte **Weiter**.  
  
4.  Klicken Sie auf **Schließen**. Das Dashboard wird neu gestartet.  
  
###  <a name="BKMK_Disable"></a> Deaktivieren der Integration von Office 365  
 Wenn Sie sich entscheiden, dass Sie keine Nachteile für Ihr Ihre Office 365-Dienste und -Onlinekonten über das Dashboard verwalten möchten, können Sie Office 365-Integration deaktivieren. Ihr Office 365-Abonnement bleibt aktiv, und über das Dashboard vorgenommenen konfigurationsänderungen bleiben bestehen. Beispielsweise erhalten Sie alle e-Mail-Adresse an, die auf einen Domänennamen, den Sie mit Ihrem Office 365-Abonnement verknüpft. Sie e-Mails verloren gehen, und Steuerelemente, die Sie für mobile Geräte festlegen, sind immer noch Exchange Online verwendet.  
  
 In Zukunft verwalten Sie Ihre Office 365-Abonnement, Dienste und Ressourcen in Office 365, und Ihre Benutzer müssen die Kennwörter für ihre Onlinekonten in Office 365 verwalten. Kennwortsynchronisierung erfolgt nicht mehr, und deaktivieren oder Entfernen eines Benutzerkontos hat keine Auswirkungen auf die Benutzer s-online-Konto.  
  
 Da die Office 365-Integrationssoftware auf dem lokalen Server installiert ist, können Sie das Feature deaktivieren, auch wenn der Integrationsdienst keine Verbindung mit Office 365 herstellen kann.  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>So deaktivieren Sie die Office 365-Integration mit dem Server  
  
1.  Klicken Sie auf dem Dashboard auf **Office 365**.  
  
2.  Klicken Sie auf **Office 365-Integration deaktivieren**. Der Assistent für das Deaktivieren von Office 365 wird angezeigt.  
  
3.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
> [!NOTE]
>  Verwenden Sie zum Aktivieren der Integration von Office 365 erneut die **in Office 365 integrieren** Aufgabe auf dem die **Service** s Dashboard-Registerkarte **Startseite** Seite. Anweisungen hierzu finden Sie unter [Schritt2: Integrieren des Windows Server Essentials-Servers mit Microsoft Office 365](#BKMK_StepTwo)weiter oben in diesem Thema.  
  
##  <a name="BKMK_Troubleshoot"></a> Problembehandlung bei Office 365-integration  
 Dieser Abschnitt enthält Informationen, mit denen Sie häufige Probleme beheben können, die auftreten können, wenn die Office 365-Integration-Features in Windows Server Essentials verwenden.  
  
###  <a name="BKMK_AcctsNotCreated"></a> Einige Microsoft Online Services-Konten wurden nicht erstellt werden.  
 **Beschreibung**  
  
 Der Versuch, ein oder mehrere Microsoft Online Services-Konten über das Dashboard war t erfolgreich zu erstellen.  
  
 **Lösung**  
  
1.  Klicken Sie auf die Abschlussseite des Assistenten, um eine Ergebnisdatei zu öffnen, die ausführliche Informationen zu jeder Anforderung zum Erstellen eines Kontos enthält, die nicht erfolgreich abgeschlossen wurde. Beispielsweise kann ein Ergebnis Ihnen aufzeigen, dass ein Microsoft Online Services-Konto mit dem Namen eines angeforderten Kontos bereits vorhanden ist.  
  
2.  Führen Sie die empfohlenen Aktionen aus, um jeden Fehler zu beheben.  
  
3.  Wenn dieses Problem weiterhin besteht, starten Sie den Server neu, und versuchen Sie, die Onlinekonten erneut zu erstellen.  
  
###  <a name="BKMK_ProblemUninstalling"></a> Es wurde ein Problem mit dem Deinstallieren von Office 365-Integration  
 **Beschreibung**  
  
 Ein Unbekannter Fehler ist aufgetreten, bei dem Versuch der Integration von Office 365 zu deaktivieren.  
  
 **Lösung**  
  
1.  Stellen Sie sicher, dass der Computer mit dem Internet verbunden ist, und versuchen Sie es erneut.  
  
2.  Wenn der Fehler erneut auftritt, starten Sie den Server neu, und versuchen Sie es erneut.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Services Integration Overview for Windows Server Essentials – Teil 1](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Services Integration Overview for Windows Server Essentials – Teil 2](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Erste Schritte für die Verwendung von Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)
