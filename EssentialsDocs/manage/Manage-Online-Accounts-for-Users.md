---
title: Verwalten von Online-Konten für Benutzer von Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.topic: article
ms.assetid: c09f4cf6-4d12-49fe-9ae4-e6cb14027b9d
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: dc3170c7d5267eef6f339dc229b1b9daaf9ac9ec
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980280"
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Verwalten von Online-Konten für Benutzer von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Ihren Windows Server Essentials-Server in Microsoft Office 365 integrieren, können Sie Ihre Online Konten zusammen mit Benutzerkonten über das Dashboard verwalten. In diesem Thema erfahren Sie, was Sie durch die Verwaltung der Microsoft Online Services-Konten von Benutzern über das Dashboard erreichen können, wie Sie Online Konten über das Dashboard erstellen und verwalten und wie Sie e-Mail-Adressen und Verteiler Gruppen für Exchange Online verwalten. über das Dashboard.  

  
> [!NOTE]
>  Um Ihre Microsoft Online Services-Konten in Windows Server Essentials verwalten zu können, müssen Sie Ihren Server in Office 365 integrieren. Anweisungen hierzu finden Sie unter [Verwalten von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md).  
  
> [!IMPORTANT]
>  Wenn Sie Online Konten in Windows Server Essentials verwalten, sind Sie daran gewöhnt, dass Microsoft Online Services-Konten als *Office 365-Konten*bezeichnet werden. Auf dem Dashboard in Windows Server Essentials wurden die Bezeichnungen in *Microsoft Online Services-Konten*oder kurz *Microsoft-Online Konten* geändert. Die Konten und die Verfahren sind identisch. Nur die Bezeichnungen wurden geändert. In den meisten Verfahren in diesem Thema wird der Begriff *Onlinekonto*verwendet.  
  
## <a name="in-this-topic"></a>In diesem Thema  
  
-   [Warum sollte ich meine Online Konten über das Dashboard verwalten?](#BKMK_WhyManageOnlineAccounts)  
  
-   [Erstellen von Online Konten](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [Verwalten von Online Konten](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Verwalten von e-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Verwalten von Verteiler Gruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a>Warum sollte ich meine Online Konten über das Dashboard verwalten?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuzuweisen, werden die Konto Kennwörter automatisch synchronisiert, und Sie können die beiden Konten während des gesamten Lebenszyklus des Benutzerkontos verwalten.  
  
 Es ist praktisch für den Benutzer, der das gleiche Kennwort für den Zugriff auf Ressourcen auf dem Server und in Office 365 verwenden kann. Außerdem können Sie die gleichen Kenn Wort Anforderungen für den Zugriff auf Ressourcen in Office 365 anwenden, die Sie für Ihre internen Ressourcen benötigen.  
  
### <a name="how-does-password-synchronization-work"></a>Wie funktioniert die Kennwortsynchronisierung?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuzuweisen, wird das Kennwort des Benutzerkontos automatisch mit dem Online Konto des Benutzers synchronisiert. Dies bedeutet, dass ein Benutzer nur ein einziges Kennwort benötigt, um auf die Ressourcen auf dem Server und in Office 365 zuzugreifen. Außerdem können Sie denselben Namen für das Benutzerkonto und die Online-ID des Benutzers verwenden.  
  
 Die Kennwortsynchronisierung erfolgt umgehend und automatisch, wenn ein Benutzer das Kennwort für das Benutzerkonto auf einem zur Domäne gehörigen Computer oder mithilfe von Remotewebzugriff ändert.  
  
> [!IMPORTANT]
>  Wenn Office 365 in Windows Server Essentials integriert ist, sollten Benutzer das Kennwort für Ihr Microsoft Online-Konto nicht über das Office 365-Portal ändern. Auf diese Weise wird die Kennwortsynchronisierung unterbrochen.  
  
### <a name="simplified-account-creation"></a>Vereinfachte Kontoerstellung  
 Es gibt einen weiteren Vorteil, wenn Sie Ihre anfänglichen Online Konten über das Dashboard erstellen. Sie können Onlinekonten für alle Benutzer mit einer einzelnen Aktion erstellen. Wenn Ihre Mitarbeiter dagegen bereits Office 365 verwenden und einen neuen Windows Server Essentials-Server einrichten, können Sie alle Benutzerkonten mit einer einzigen Aktion aus den Online Konten erstellen. Weitere Informationen finden Sie unter [Erstellen von Onlinekonten](#BKMK_SECTION_CreateOnlineAccounts).  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>Verwalten von E-Mail-Adressen und Verteilergruppen über das Dashboard  
 Sie können E-Mail-Adressen und Verteilergruppen für Exchange Online über das Dashboard verwalten. Und Sie können die Internet Domäne Ihrer Organisation in den e-Mail-Adressen verwenden. Sie können all dies über das Dashboard ausführen, ohne sich bei Office 365 anzumelden. (Sie müssen Windows Server Essentials verwenden, um Verteiler Gruppen über das Dashboard zu verwalten. Diese Funktion wird in Windows Server Essentials nicht unterstützt.) Weitere Informationen finden Sie unter [Verwalten von E-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses) und [Verwalten von Verteilergruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups).  
  
### <a name="manage-the-user-account-and-online-account-together"></a>Gemeinsames Verwalten von Benutzerkonto und Onlinekonto  
 Und Sie können ein Onlinekonto zusammen mit dem Benutzerkonto während des gesamten Lebenszyklus des Kontos verwalten. Wenn Sie das Benutzerkonto deaktivieren, wird das Onlinekonto in Microsoft Online Services ebenfalls deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](#BKMK_SECTION_ManageOnlineAccounts).  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a>Erstellen von Online Konten  
 Nachdem Sie Ihren Server in Office 365 integriert haben, ist es zu Ihrem Vorteil, Microsoft Online Services-Konten für Ihre Benutzer über das Dashboard zu erstellen. Sie haben viel Flexibilität bei der Erstellung der Online Konten. Wenn Sie über ein neues Office 365-Abonnement verfügen, können Sie Online Konten für alle Benutzer per Massen Vorgang erstellen. Wenn Sie Ihre Online Konten in Office 365 bereits erstellt haben, machen Sie sich keine Sorgen. Wenn Sie einen neuen Server einrichten, können Sie die Benutzerkonten auf dem Server erstellen, indem Sie die Online Konten importieren. Sie können entweder ein neues oder ein vorhandenes Onlinekonto zuweisen, wenn Sie ein einzelnes Benutzerkonto erstellen, oder wenn Sie ein Onlinekonto einem vorhandenen Benutzerkonto hinzufügen.  
  
 **Lizenzanforderungen** Sie benötigen eine Benutzerlizenz für jedes von Ihnen erstellte Onlinekonto. Überprüfen Sie auf dem Dashboard die Seite **Office 365** , um zu sehen, wie viele Benutzerlizenzen über Ihr Office 365-Abonnement zur Verfügung stehen. Wenn Sie weitere Benutzerlizenzen hinzufügen müssen, können Sie Ihr Office 365-Abonnement in Office 365 öffnen, um dies zu tun.  
  
 **Nachverfolgung für Benutzer** Nachdem Sie ein Onlinekonto für ein Benutzerkonto hinzugefügt haben, muss der Benutzer das Kennwort für sein Benutzerkonto bei der nächsten Anmeldung ändern. Das neue Kennwort wird sofort mit dem Onlinekonto synchronisiert. Danach können Sie das Kennwort verwenden, um sich mit Ihrer Online-ID bei Office 365 anzumelden.  
  
> [!IMPORTANT]
>  Betonen Sie für Ihre Benutzer, dass Sie Ihr Onlinekonto Kennwort in Office 365 niemals ändern sollten. Das Kennwort wird immer dann automatisch geändert, wenn sie das Kennwort für ihr Benutzerkonto ändern. Wenn Sie das Online Kennwort in Office 365 ändern, wird die Kenn Wort Synchronisierung abgebrochen.  
  
 Verwenden Sie die Verfahren in diesem Abschnitt für Folgendes:  
  
-   [Erstellen Sie Online Konten für vorhandene Benutzerkonten per Massen Vorgang.](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Importieren von Benutzerkonten aus Ihren Microsoft Online Services-Konten](#BKMK_ToImportUserAccounts)  
  
-   [Erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto.](#BKMK_ToCreateaNewUserAccount)  
  
-   [Zuweisen eines Online Kontos zu einem Benutzerkonto](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  Wenn Sie Windows Server Essentials verwenden, wird in diesem Verfahren das *Office 365-Konto* anstelle des *Microsoft Online Services-Kontos* angezeigt. Der Prozess ist identisch, aber die Terminologie wurde in Windows Server Essentials geändert.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a>So erstellen Sie Online Konten für vorhandene Benutzerkonten per Massen Vorgang  
  
1.  Melden Sie sich auf dem Server als Administrator an, und öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Öffnen Sie auf dem Dashboard die Seite **Benutzer**.  
  
3.  Klicken Sie unter **Benutzeraufgaben** auf **Microsoft Onlinekonten hinzufügen**.  
  
     Die Seite **Microsoft Online Services-Konten hinzufügen** des Assistenten zeigt alle Benutzerkonten, die nicht über ein Microsoft Onlinekonto verfügen. Alle Konten sind standardmäßig ausgewählt, und der Benutzername wird für die Microsoft Online-ID empfohlen. Wenn Sie eine benutzerdefinierte Internet Domäne mit Ihrem Office 365-Abonnement verknüpft haben, wird diese Domäne standardmäßig verwendet.  
  
4.  Prüfen Sie auf der Seite **Microsoft Online Services-Konten hinzufügen** die Konten, die erstellt werden. Prüfen Sie z. B. auf Benutzer, die bereits ein Onlinekonto mit einer anderen Online-ID besitzen, und stellen Sie sicher, dass die Domäne, die Sie in E-Mail-Adressen verwenden möchten, ausgewählt ist. Wenn Sie alle erforderlichen Änderungen vorgenommen haben, klicken Sie auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Microsoft Online Services-Lizenzen zuweisen** die Office 365-Dienste aus, die Ihre Benutzer verwenden werden. Wenn Sie auf **Weiter** klicken, wird die Kontoerstellung gestartet.  
  
    > [!NOTE]
    >  Sie müssen für jedes Onlinekonto über eine Dienst Lizenz in Office 365 verfügen. Sie können die verfügbaren Lizenzen überprüfen und können ggf. das Abonnement zum Hinzufügen von Lizenzen von der **Office 365** -Seite des Dashboards öffnen.  
  
6.  Benachrichtigen Sie die Benutzer, dass sie nun über ein Microsoft Onlinekonto verfügen. Sie müssen Ihr Kennwort für das Netzwerk Benutzerkonto ändern, bevor Sie sich bei Office 365 anmelden können. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a>So beginnen Sie mit der Verwendung eines neuen Microsoft Online Kontos  
  
1.  Melden Sie sich auf dem Computer mit dem Netzwerkbenutzerkonto an.  
  
2.  Ändern Sie das Kennwort für das Benutzerkonto. Drücken Sie zuerst STRG+ALT+ENTF, und klicken Sie dann auf **Kennwort ändern**.  
  
     Wenn Sie Ihr Kennwort ändern, wird das Kennwort mit dem neuen Onlinekonto synchronisiert. Sie können jetzt dasselbe Kennwort verwenden, um sich bei Office 365 anzumelden.  
  
3.  [Melden Sie sich bei Office 365](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) mit Ihrer neuen Online-ID und dem Kennwort Ihres Benutzerkontos an.  
  
    > [!IMPORTANT]
    >  Ändern Sie das Kennwort Ihres Online Kontos nicht in Office 365. Auf diese Weise wird die Kennwortsynchronisierung unterbrochen. Ihr Onlinekennwort wird jedes Mal aktualisiert, wenn Sie das Kennwort für das Netzwerkbenutzerkonto ändern.  
  
###  <a name="BKMK_ToImportUserAccounts"></a>So importieren Sie Benutzerkonten aus Ihren vorhandenen Online Konten  
  
1.  Öffnen Sie auf dem Dashboard die Seite **Benutzer**.  
  
2.  Klicken Sie unter **Benutzeraufgaben**auf **Konten aus Office 365 importieren**.  
  
     Auf der nächsten Seite werden alle Online Konten für Ihr Office 365-Abonnement angezeigt, die nicht über ein Benutzerkonto auf dem Server verfügen. Alle Konten sind standardmäßig ausgewählt, und die Online-ID wird als Benutzername vorgeschlagen.  
  
3.  So erstellen Sie die Benutzerkonten:  
  
    1.  Nehmen Sie alle erforderlichen Änderungen an den vorgeschlagenen Benutzerkonten vor.  
  
    2.  Klicken Sie optional auf den Link, um die temporären Kennwörter anzuzeigen, die den Benutzerkonten zugewiesen werden. Sie müssen den Benutzern ihre temporären Kennwörter zusammen mit ihren neuen Kontonamen mitteilen.  
  
         (Nachdem Sie die Konten erstellt haben, finden Sie diese Kenn Wörter in der folgenden Datei: *System Drive*\Users\\*Office365admin*\\*newserveruser*. txt, wobei *Office365admin* das Netzwerk Konto ist, das zum Verwalten von Office 365 auf dem Server verwendet wird, und *newserveruser* ist das neue Name des Benutzerkontos.)  
  
    3.  Klicken Sie auf **Weiter** , um die Benutzerkonten zu erstellen.  
  
4.  Informieren Sie Ihre Benutzer über Ihre neuen Benutzerkonten und die temporären Kenn Wörter, die Sie für die erstmalige Anmeldung beim Server verwenden werden, und dass Sie das Kennwort nach der Anmeldung ändern müssen. Anweisungen finden Ihre Benutzer unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
     Stellen Sie sicher, dass die Kenn Wörter für Ihr Onlinekonto mit Ihrem Benutzerkonto synchronisiert werden, und dass Sie Ihr Online Kennwort in Office 365 nicht ändern sollten.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a>So erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie unter **Benutzeraufgaben**auf **Benutzerkonto hinzufügen**. Der Assistent für das Hinzufügen eines Benutzerkontos wird angezeigt.  
  
3.  Folgen Sie den Anweisungen, um das Benutzerkonto zu erstellen.  
  
4.  Erstellen Sie auf der Seite **Ein Microsoft Online Services-Konto zuweisen** entweder ein neues Onlinekonto für den Benutzer oder weisen Sie ein vorhandenes Onlinekonto zu:  
  
    -   Klicken Sie zum Erstellen eines neuen Onlinekontos auf **Ein neues Microsoft Online Services-Konto erstellen und diesem Benutzerkonto zuweisen**, und geben Sie einen Namen für das Microsoft Online Services-Konto ein. (Standardmäßig wird der Benutzername für die Online-ID verwendet.) Klicken Sie dann auf **Weiter**.  
  
    -   Klicken Sie auf **Ein vorhandenes Microsoft Online Services-Konto diesem Benutzerkonto zuweisen**, um ein vorhandenes Microsoft Onlinekonto zuzuweisen, und wählen Sie ein vorhandenes Konto aus der Dropdownliste aus. Klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  In Windows Server Essentials werden Microsoft Online Services-Konten in Assistenten und dashboardbezeichnungen als Office 365-Konten bezeichnet.  
  
5.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
6.  Benachrichtigen Sie den Benutzer, dass er das Kennwort des Benutzerkontos ändern muss, bevor er sich bei Office 365 mit dem neuen Onlinekonto anmelden kann. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>So weisen Sie ein Onlinekonto einem Benutzerkonto zu  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Ein Microsoft Onlinekonto zuweisen**. Der Assistent für die Zuweisung eines Microsoft Online Services-Kontos wird angezeigt.  
  
3.  Weisen Sie ein vorhandenes Onlinekonto zu, oder erstellen Sie ein neues für den Benutzer. Die Standard-Online-ID für ein neues Konto ist der Benutzername. Klicken Sie dann auf **Weiter** , um das Onlinekonto dem Benutzerkonto hinzuzufügen.  
  
4.  Überprüfen Sie die Informationen auf der letzten Seite des Assistenten, und klicken Sie dann auf **Schließen**.  
  
5.  Benachrichtigen Sie den Benutzer, dass er das Kennwort des Benutzerkontos ändern muss, bevor er sich bei Office 365 mit dem neuen Onlinekonto anmelden kann. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a>Verwalten von Online Konten  
 Wenn Sie einem Benutzerkonto in Windows Server Essentials ein Onlinekonto hinzufügen, können Sie beide Konten während des gesamten Lebenszyklus des Kontos verwalten.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a>Grundlegendes zum Status des Online Kontos  
 Wenn Sie ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, wird die E-Mail-Adresse für das Konto in der **Microsoft Onlinekonto**-Spalte auf der Seite **Benutzer** des Dashboards angezeigt. (In Windows Server Essentials lautet die Spalten Bezeichnung **Office 365-Konto**.)  
  
-   Ein blaues Symbol neben einer E-Mail-Adresse gibt an, dass das Onlinekonto aktiv ist. Das Konto verfügt über eine aktuelle Office 365-Lizenz, und der Benutzer kann die Online-ID verwenden, um sich bei Office 365 anzumelden.  
  
-   Ein schattiertes Symbol neben der e-Mail-Adresse gibt an, dass das Onlinekonto inaktiv ist. Dies geschieht entweder, weil die Lizenz nicht mehr aktiv ist oder das Onlinekonto nicht zugewiesen wurde. Wenn Sie die Zuweisung eines Online Kontos des Benutzers aufheben, wird die Lizenz entfernt, und der Benutzer wird daran gehindert, sich mit dem Konto bei Office 365 anzumelden. Der Server behält jedoch die Zuordnung zwischen dem Benutzerkonto Namen und der Office 365-e-Mail-Adresse bei.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a>Beschränken des Zugriffs auf ein Onlinekonto  
 Was tun Sie, wenn ein Benutzer Ihre Organisation verlässt oder Sie den Zugriff des Benutzers auf Ihre Office 365-Dienste einschränken möchten? Wenn Sie Ihre Benutzer Online Konten zusammen mit ihren Benutzerkonten in Windows Server Essentials verwalten, stehen Ihnen drei Optionen zur Verfügung:  
  
-   **Zuweisung des Online Kontos** aufheben? Wenn Sie einen Benutzer daran hindern möchten, Office 365 zu verwenden, ohne den Zugriff auf Ressourcen auf dem Server zu verhindern, sollten Sie die Zuweisung des Online Kontos aufheben. Die Office 365-Lizenz wird freigegeben, und der Benutzer wird daran gehindert, sich bei Office 365 anzumelden. Der Server behält jedoch die Zuordnung zwischen dem Benutzerkonto Namen und der Office 365-e-Mail-Adresse bei. Anweisungen finden [Sie unter So heben Sie die Zuweisung eines Online Kontos zu einem Benutzerkonto auf](#BKMK_ToUnassignAnOnlineAccount).  
  
-   **Benutzerkonto deaktivieren** ? Wenn Sie ein Benutzerkonto deaktivieren, weil ein Mitarbeiter entweder vorübergehend oder dauerhaft verlässt, wird das Onlinekonto des Benutzers ebenfalls deaktiviert. Das Onlinekonto kann nicht verwendet werden, aber die Benutzerdaten, einschließlich E-Mails, werden in Microsoft Online Services beibehalten. Anweisungen hierzu finden Sie unter [Deaktivieren eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) in [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
-   **Entfernen Sie das Benutzerkonto** ? Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls aus Microsoft Online Services entfernt. Anweisungen hierzu finden Sie unter [Entfernen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) in [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
    > [!WARNING]
    >  Beachten Sie, dass bei einer Entfernung eines Onlinekontos die Benutzerdaten den Datenaufbewahrungsrichtlinien von Microsoft Online Services unterliegen. Wenn Sie die Benutzerdaten der Person beibehalten müssen, nachdem ein Mitarbeiter das Unternehmen verlassen hat, deaktivieren Sie das Benutzerkonto, anstatt es zu entfernen.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a>So heben Sie die Zuweisung eines Online Kontos zu einem Benutzerkonto auf  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Zuweisung eines Microsoft Online Kontos** aufheben (in Windows Server Essentials auf **Zuweisung eines Office 365-Kontos**aufheben).  
  
3.  Klicken Sie bei der Bestätigungsaufforderung auf **Ja**.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a>Verwalten von e-Mail-Adressen für Exchange Online  
 Durch das Hinzufügen von e-Mail-Adressen zum Onlinekonto des Benutzers in Windows Server Essentials können Sie es dem Benutzer ermöglichen, e-Mails über mehrere e-Mail-Adressen in Exchange Online zu erhalten.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a>So fügen Sie einem Microsoft Onlinekonto eines Benutzers zusätzliche e-Mail-Adressen hinzu  
  
1.  Klicken Sie im Windows Server Essentials-Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Klicken Sie auf der Registerkarte **Microsoft Online** in den Konto Eigenschaften (bzw. auf der Registerkarte **Office 365** in Windows Server Essentials) auf **Hinzufügen**.  
  
4.  Geben Sie den neuen E-Mail-Alias ein, und wählen Sie dann die E-Mail-Domäne aus.  
  
5.  Klicken Sie zweimal auf **OK** .  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a>Verwalten von Verteiler Gruppen für Exchange Online (nur Windows Server Essentials)  
 Nachdem Sie Ihren Windows Server Essentials-Server in Office 365 integriert haben, können Sie Verteiler Gruppen für Exchange Online über das Windows Server Essentials-Dashboard erstellen und verwalten. Dies erfolgt auf der Registerkarte **Verteiler Gruppen** , die der Seite **Benutzer** hinzugefügt wird. Diese Registerkarte wird nur angezeigt, wenn Sie über ein Exchange Online-Abonnement verfügen. Diese Funktion ist in Windows Server Essentials nicht verfügbar.  
  
 Verwenden Sie die folgenden Verfahren für Folgendes:  
  
-   [Hinzufügen einer Verteiler Gruppe](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [Ändern der Mitglieder einer Verteiler Gruppe](#BKMK_ChangeGroupMembers)  
  
-   [Ändern der Verteiler Gruppenmitgliedschaften eines Benutzers](#BKMK_EditUserMemberships)  
  
-   [Entfernen einer Verteiler Gruppe](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a>So fügen Sie eine Verteiler Gruppe hinzu  
  
1.  Klicken Sie im Dashboard in Windows Server Essentials auf **Benutzer**, und klicken Sie dann auf die Registerkarte **Verteiler Gruppen** .  
  
2.  Klicken Sie unter **Verteilergruppenaufgaben**auf **Eine Verteilergruppe hinzufügen**.  
  
     Der Assistent für das Hinzufügen einer neuen Verteilergruppe wird angezeigt.  
  
3.  Geben Sie die folgenden Informationen auf der Seite **Eine neue Verteilergruppe hinzufügen** ein, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie einen Gruppennamen, die Beschreibung und den E-Mail-Alias für die neue Verteilergruppe ein.  
  
    -   Standardmäßig kann die Verteilergruppe E-Mails von Personen außerhalb Ihrer Organisation empfangen. Wenn dies nicht möglich sein soll, deaktivieren Sie diese Option.  
  
4.  Verwenden Sie auf der Seite **Gruppenmitglieder hinzufügen** die Schaltfläche **Hinzufügen**, um aktive Benutzerkonten, denen ein Onlinekonto zugewiesen wurde, und andere Verteilergruppen zur neuen Verteilergruppe hinzuzufügen. Klicken Sie dann auf **Weiter**.  
  
     In Exchange Online wird die neue Verteilergruppe erstellt.  
  
###  <a name="BKMK_ChangeGroupMembers"></a>So ändern Sie die Mitglieder einer Verteiler Gruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**und dann auf die Registerkarte **Verteilergruppen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **Ändern der Gruppenmitgliedschaft**.  
  
3.  Verwenden Sie die Schaltflächen **Hinzufügen** und **Entfernen** , um aktive Onlinekonten zur Verteilergruppe hinzuzufügen oder daraus zu entfernen. Klicken Sie dann auf **Weiter**, um die Verteilergruppenmitgliedschaft in Exchange Online zu aktualisieren.  
  
###  <a name="BKMK_EditUserMemberships"></a>So ändern Sie die Verteiler Gruppenmitgliedschaften eines Benutzers  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Klicken Sie in den Eigenschaften des Benutzerkontos auf die Registerkarte **Verteilergruppen**, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Verwenden Sie im Feld **Gruppenmitgliedschaft bearbeiten** die Schaltflächen **Hinzufügen** und **Entfernen** , um Verteilergruppen zum Benutzerkonto hinzuzufügen oder daraus zu entfernen, und klicken Sie dann auf **Schließen**.  
  
5.  Klicken Sie auf **OK**, um die aktualisierten Benutzerkontoeigenschaften zu speichern.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a>So entfernen Sie eine Verteiler Gruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**und dann auf die Registerkarte **Verteilergruppen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **Gruppe entfernen**.  
  
3.  Klicken Sie bei der Bestätigungsaufforderung auf **Gruppe löschen**.  
  
     Die Verteilergruppe wird aus Exchange Online entfernt.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
