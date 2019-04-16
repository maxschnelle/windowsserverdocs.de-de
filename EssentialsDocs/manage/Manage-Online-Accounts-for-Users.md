---
title: "Verwalten von Online-Konten für Benutzer von Windows Server Essentials"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c09f4cf6-4d12-49fe-9ae4-e6cb14027b9d
8author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 95f401bbec9bb503d19e2d9918a05851c04f7ef4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Verwalten von Online-Konten für Benutzer von Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Wenn Sie Ihre Windows Server Essentials-Server mit Microsoft Office365 integrieren, können Sie Ihre Onlinekonten und Benutzerkonten über das Dashboard verwalten. In diesem Thema finden Sie alles, welche Vorteile Sie durch die Benutzer Microsoft Online Services-Konten über das Dashboard verwalten, erstellen und Verwalten von Onlinekonten über das Dashboard und wie Sie E-Mail-Adressen und Verteilergruppen für Exchange Online über das Dashboard verwalten.  

  
> [!NOTE]
>  Um Ihre Microsoft Online Services-Konten in Windows Server Essentials zu verwalten, müssen Sie den Server mit Office365 integrieren. Anweisungen finden Sie unter [Verwalten von Office365](Manage-Office-365-in-Windows-Server-Essentials.md).  
  
> [!IMPORTANT]
>  Wenn Sie Verwalten von Online-Konten in Windows Server Essentials, Sie daran gewöhnt, dass Microsoft Online Services-Konten, die so genannte *Office365-Konten*. Auf dem Dashboard in Windows Server Essentials die Bezeichnungen wurden geändert wurden *Microsoft Online Services-Konten*, oder *Microsoft-Onlinekonten* kurz. Die Konten und die Verfahren sind identisch. nur die Bezeichnungen geändert. Die meisten Verfahren in diesem Thema verwenden den Begriff *Onlinekonto*.  
  
## <a name="in-this-topic"></a>In diesem Thema  
  
-   [Warum sollte ich meine Onlinekonten über das Dashboard verwalten?](#BKMK_WhyManageOnlineAccounts)  
  
-   [Erstellen von Onlinekonten](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [Verwalten von Onlinekonten](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Verwalten von E-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Verwalten von Verteilergruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a>Warum sollte ich meine Onlinekonten über das Dashboard verwalten?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, die Kennwörter werden automatisch synchronisiert, und die beiden Konten gemeinsam im gesamten Benutzer Konto s Lebenszyklus verwaltet werden können.  
  
 Es ist praktisch für die Benutzer, dasselbe Kennwort zum Zugriff auf Ressourcen auf dem Server und in Office365 verwenden kann. Und Sie können die gleichen Kennwortanforderungen wie für den Zugriff auf Ressourcen in Office365, die Sie für internen Ressourcen benötigen.  
  
### <a name="how-does-password-synchronization-work"></a>Wie funktioniert die kennwortsynchronisierung?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, wird das Kennwort des Benutzerkontos automatisch mit dem Onlinekonto des Benutzers s synchronisiert. Dies bedeutet, dass ein Benutzer nur Zugriff auf die Ressourcen auf dem Server und in Office365 ein einziges Kennwort benötigt. Darüber hinaus können Sie den gleichen Namen für das Benutzerkonto und die Benutzer s-Online-ID verwenden.  
  
 Synchronisierung von Kennwörtern tritt unmittelbar und automatisch, wenn ein Benutzer das Kennwort für ihr Konto über einen Computer einer Domäne oder mit Remote Web Access ändert.  
  
> [!IMPORTANT]
>  Wenn Windows Server Essentials Office365 integriert ist, sollten Benutzer das Kennwort für ihr Microsoft Onlinekonto aus Office365-Portal nicht ändern. Auf diese Weise wird die kennwortsynchronisierung unterbrochen.  
  
### <a name="simplified-account-creation"></a>Vereinfachte kontoerstellung  
 Es ist ein weiterer Vorteil bei der Erstellung der ursprünglichen Onlinekonten über das Dashboard. Sie können Onlinekonten für alle Benutzer mit einer einzelnen Aktion erstellen. Andererseits, können, wenn Ihre Mitarbeiter bereits von Office365 verwendet werden, und Sie einen neuen Windows Server Essentials-Server einrichten, Sie alle Benutzerkonten aus den Onlinekonten mit einer einzelnen Aktion erstellen. Weitere Informationen finden Sie unter [Erstellen von Onlinekonten](#BKMK_SECTION_CreateOnlineAccounts).  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>Verwalten von E-Mail-Adressen und Verteilergruppen über das Dashboard  
 Sie werden Ihre E-Mail-Adressen und Verteilergruppen für Exchange Online über das Dashboard verwalten können. Und Sie können Ihre Organisation s Internetdomäne die E-Mail-Adressen verwenden. Sie können all diese über das Dashboard tun, ohne Anmeldung bei Office365. (Sie muss auf Windows Server Essentials verwenden, um Verteilergruppen über das Dashboard verwalten. Dieses Feature ist nicht in Windows Server Essentials unterstützt.) Weitere Informationen finden Sie unter [Verwalten von E-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses) und [Verwalten von Verteilergruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups).  
  
### <a name="manage-the-user-account-and-online-account-together"></a>Das Benutzerkonto und Onlinekonto zusammen verwalten  
 Und Sie Onlinekonten zusammen mit dem Benutzerkonto während des Lebenszyklus des Kontos s verwalten können. Wenn Sie das Benutzerkonto deaktivieren, wird das Onlinekonto in Microsoft Online Services ebenfalls deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](#BKMK_SECTION_ManageOnlineAccounts).  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a>Erstellen von Onlinekonten  
 Nachdem Sie den Server mit Office365 integrieren, ist es von Vorteil, Microsoft Online Services-Konten für die Benutzer über das Dashboard zu erstellen. Sie müssen ein hohes Maß an Flexibilität bei der Erstellung der Onlinekonten. Wenn Sie ein neues Office365-Abonnement verfügen, können Sie per Massenimport-Online-Konten für alle Benutzer erstellen. Wenn Sie bereits Onlinekonten in Office365 erstellt haben, kein Problem. Wenn Sie einen neuen Server einrichten, Sie die Benutzerkonten auf dem Server erstellen können, indem Sie die Onlinekonten importieren. Und Sie können ein neues oder ein vorhandenes Onlinekonto zuweisen, wenn Sie ein einzelnes Benutzerkonto erstellen, oder wenn Sie ein Onlinekonto zu einem vorhandenen Benutzerkonto hinzufügen.  
  
 **Lizenzanforderungen** benötigen Sie eine Benutzerlizenz für jedes Onlinekonto an, die Sie erstellen. Überprüfen Sie die **Office365** -Seite des Dashboards, wie viele Benutzerlizenzen über Ihr Office365-Abonnement verfügbar sind. Wenn Sie weitere Lizenzen für Benutzer hinzufügen müssen, werden Sie alles Office365-Abonnement in Office365 zu diesem Zweck öffnen.  
  
 **Anschlussmaßnahme für Benutzer** ein Onlinekonto für ein Benutzerkonto hinzugefügt haben, ist der Benutzer erforderlich, um das Kennwort für ihr Konto ändern, das nächste Mal anmelden. Das neue Kennwort wird sofort mit dem Onlinekonto synchronisiert. Danach können sie das Kennwort verwenden, zum Anmelden bei Office365 mit ihrer Online-ID  
  
> [!IMPORTANT]
>  Betonen Sie die Benutzer, dass sie ihr Kennwort Online-Konto in Office365 nie ändern sollten. Das Kennwort wird automatisch geändert werden, wenn sie das Kennwort für dieses Benutzerkonto ändern. Wenn sie das Onlinekennwort in Office365 geändert werden, wird die kennwortsynchronisierung unterbrochen werden.  
  
 Verwenden Sie die Verfahren in diesem Abschnitt:  
  
-   [Erstellen Sie Onlinekonten für vorhandene Benutzerkonten per Massenimport](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Importieren Sie Benutzerkonten aus Ihren Microsoft Online Services-Konten](#BKMK_ToImportUserAccounts)  
  
-   [Erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto](#BKMK_ToCreateaNewUserAccount)  
  
-   [Zuweisen eines Onlinekontos zu einem Benutzerkonto](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  Wenn Sie mit Windows Server Essentials, angezeigt wird, *Office365-Konto* anstelle von *Microsoft Online Services-Konto* während dieses Vorgangs. Der Prozess ist identisch, aber die Terminologie in Windows Server Essentials.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a>Um die Onlinekonten für vorhandene Benutzerkonten per Massenimport erstellen  
  
1.  Melden Sie sich auf dem Server als Administrator, und öffnen Sie das Windows Server Essentials-Dashboard.  
  
2.  Öffnen Sie auf dem Dashboard die **Benutzer** Seite.  
  
3.  In **Benutzeraufgaben**, klicken Sie auf **Microsoft Onlinekonten hinzufügen**.  
  
     Die **Microsoft Online Services-Konten hinzufügen** Seite des Assistenten zeigt alle Benutzerkonten, die nicht über ein Microsoft-Onlinekonto verfügen. Alle Konten sind standardmäßig ausgewählt, und der Benutzername wird für die Microsoft-Online-ID Wenn Sie eine benutzerdefinierte Internetdomäne mit Ihrem Office365-Abonnement verknüpft haben, wird standardmäßig diese Domäne verwendet werden.  
  
4.  Auf der **Microsoft Online Services-Konten hinzufügen** Seite, überprüfen Sie die Konten, die erstellt wird. Überprüfen Sie z.B. für Benutzer, die bereits ein Onlinekonto mit einer anderen Online-ID besitzen, und stellen Sie sicher, dass die Domäne, die Sie in E-Mail-Adressen verwenden möchten, ausgewählt ist. Wenn Sie nach Abschluss einer Änderungen erforderlich, klicken Sie auf **Weiter**.  
  
5.  Auf der **Zuweisen von Microsoft Online Services-Lizenzen** Seite, wählen Sie Office365-Dienste, die Ihre Benutzer verwenden. Beim Klicken auf **Weiter**, kontoerstellung wird gestartet.  
  
    > [!NOTE]
    >  Sie müssen eine Dienstlizenz in Office365 für jedes Onlinekonto verfügen. Sie können die verfügbaren Lizenzen überprüfen, öffnen Sie gegebenenfalls das Abonnement zum Hinzufügen von Lizenzen von der **Office365** -Seite des Dashboards.  
  
6.  Benachrichtigen Sie Benutzer, dass sie jetzt ein Microsoft-Onlinekonto verfügen. Sie müssen das Kennwort für ihr Netzwerk ändern, bevor sie mit Office365 anmelden können. Anweisungen finden Sie unter [erste Schrittemit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a>Erste Schrittemit dem neuen Microsoft Onlinekonto  
  
1.  Melden Sie sich auf Ihrem Computer mit dem Netzwerkbenutzerkonto an.  
  
2.  Ändern Sie das Kennwort für Ihr Benutzerkonto. Um zu beginnen, drücken Sie Strg+Alt+Entf, und klicken Sie auf **Ändern eines Kennworts**.  
  
     Wenn Sie Ihr Kennwort ändern, wird das Kennwort mit dem neuen Onlinekonto synchronisiert. Jetzt können Sie dasselbe Kennwort verwenden, bei Office365 anmelden.  
  
3.  [Melden Sie sich bei Office365](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) mit Ihrer neuen Online-ID und das Kennwort Ihres Benutzerkontos.  
  
    > [!IMPORTANT]
    >  Ändern Sie das Kennwort Ihres Onlinekontos in Office365 nicht. Die wird die kennwortsynchronisierung unterbrochen. Ihr Onlinekennwort wird jedes Mal aktualisiert Sie das Kennwort für Ihr Netzwerkbenutzerkonto ändern.  
  
###  <a name="BKMK_ToImportUserAccounts"></a>So importieren Sie Benutzerkonten aus Ihren vorhandenen Onlinekonten  
  
1.  Öffnen Sie auf dem Dashboard die **Benutzer** Seite.  
  
2.  In **Benutzeraufgaben**, klicken Sie auf **Konten aus Office365 importieren**.  
  
     Die nächste Seite zeigt alle Onlinekonten für Office365-Abonnement, die nicht über ein Benutzerkonto auf dem Server verfügen. Alle Konten sind standardmäßig ausgewählt, und die Online-ID wird für den Benutzernamen vorgeschlagen.  
  
3.  So erstellen Sie die Benutzerkonten:  
  
    1.  Stellen Sie alle Änderungen, die den vorgeschlagenen Benutzerkonten erforderlich sind.  
  
    2.  Klicken Sie optional auf den Link, um die temporären Kennwörter anzuzeigen, die den Benutzerkonten zugewiesen werden soll. Sie müssen den Benutzern ihre temporären Kennwörter zusammen mit dem Namen des neuen Kontos erteilen.  
  
         (Nachdem Sie die Konten erstellt haben, finden Sie alle diese Kennwörter in dieser Datei aufgeführt: *SystemDrive*\Users\\*Office365admin*\\*NewServerUser*txt, in denen *Office365admin* das Netzwerkkonto, das zum Verwalten von Office365 auf dem Server verwendet wird und *NewServerUser* ist der Name des neuen Benutzerkontos.)  
  
    3.  Klicken Sie auf **Weiter** die Benutzerkonten erstellen.  
  
4.  Ermöglichen Sie Benutzern ihre neue Benutzerkonten sowie die temporären Kennwörter verwenden, melden Sie sich auf dem Server für das erste Mal œ und, die das Kennwort zu ändern, nachdem sie sich anmelden müssen. Anweisungen finden Ihre Benutzer finden Sie unter [erste Schrittemit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
     Achten Sie darauf, dass Benutzer wissen, dass ihr Konto in Zukunft die Kennwörter für ihre Online-Konto synchronisiert werden und sie sollten ihr Onlinekennwort in Office365 nicht ändern.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a>Erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  In **Benutzeraufgaben**, klicken Sie auf **Hinzufügen eines Benutzerkontos**. Die Add a User Account Wizard angezeigt wird.  
  
3.  Führen Sie die Anweisungen, um das Benutzerkonto zu erstellen.  
  
4.  Auf der **Zuweisen eines Microsoft Online Services-Kontos** Seite entweder erstellen Sie ein neues Online-Konto für den Benutzer oder ein vorhandenes Onlinekonto zuweisen:  
  
    -   Um ein neues Onlinekonto zu erstellen, klicken Sie auf **ein neues Microsoft Online Services-Konto erstellen und diesem Benutzerkonto zuweisen**, und geben Sie einen Namen für das Microsoft Online Services-Konto (in der Standardeinstellung wird der Benutzername für die Online-ID verwendet). Klicken Sie dann auf **Weiter**.  
  
    -   Um ein vorhandenes Microsoft Onlinekonto zuzuweisen, klicken Sie auf **ein vorhandenes Microsoft Online Services-Konto diesem Benutzerkonto zuweisen**, und wählen Sie ein vorhandenes Konto aus der Dropdownliste. Klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Microsoft Online Services-Konten werden in Windows Server Essentials als Office365-Konten im Assistenten und Dashboard bezeichnet.  
  
5.  Führen Sie die Anweisungen, um den Assistenten abzuschließen.  
  
6.  Benachrichtigen des Benutzers, den sie benötigen das Kennwort für ihr zu ändern, bevor sie mit Office365 mit dem neuen Onlinekonto anmelden können. Anweisungen finden Sie unter [erste Schrittemit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>Ein Benutzerkonto ein Onlinekonto zuweisen  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **zuweisen ein Microsoft Onlinekontos**. Die Zuweisung wird eine Microsoft Online Services-Konto-Assistenten angezeigt.  
  
3.  Weisen Sie ein vorhandenes Onlinekonto zu, oder erstellen Sie ein neues Konto für den Benutzer. Die Standard-Online-ID für ein neues Konto ist der Benutzername. Klicken Sie dann auf **Weiter** das Onlinekonto dem Benutzerkonto hinzufügen.  
  
4.  Überprüfen Sie die Informationen auf der letzten Seite des Assistenten, und klicken Sie dann auf **schließen**.  
  
5.  Benachrichtigen des Benutzers, den sie benötigen das Kennwort für ihr zu ändern, bevor sie mit Office365 mit dem neuen Onlinekonto anmelden können. Anweisungen finden Sie unter [erste Schrittemit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a>Verwalten von Onlinekonten  
 Wenn Sie ein Benutzerkonto in Windows Server Essentials ein Onlinekonto hinzufügen, können Sie beide Konten während des Lebenszyklus des Kontos s zusammen verwalten.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a>Grundlegendes zum Status des Onlinekontos  
 Wenn Sie ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, die E-Mail-Adresse für das Konto wird angezeigt, der **Microsoft-Onlinekonto** Spalte auf den **Benutzer** -Seite des Dashboards. (In Windows Server Essentials ist die Bezeichnung der Spalte **Office365-Konto**.)  
  
-   Ein blaues Symbol neben einer E-Mail-Adresse gibt an, dass das Onlinekonto aktiv ist. Das heißt, das Konto verfügt über eine aktuelle Office365-Lizenz, und der Benutzer kann die Online-ID zum Anmelden bei Office365 verwenden.  
  
-   Ein schattiertes Symbol neben der E-Mail-Adresse gibt an, das Onlinekonto inaktiv œ entweder ist, da die Lizenz nicht mehr aktiv ist oder das Onlinekonto nicht zugewiesen wurde. Wenn Sie ein Onlinekonto des Benutzers s aufheben, die Lizenz entfernt und der Benutzer aus anmelden bei Office365 über das Konto gesperrt ist. Der Server behält jedoch die Zuordnung zwischen den Namen des Benutzerkontos und der Office365 E-Mail-Adresse.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a>Einschränken des Zugriffs auf ein Onlinekonto  
 Wie gehen Sie vor, wenn ein Benutzer die Organisation verlässt oder Sie den Benutzer s den Zugriff auf Ihre Office365-Dienste einschränken möchten? Verwalten von Benutzern Onlinekonten zusammen mit den Benutzerkonten in Windows Server Essentials, Sie drei Möglichkeiten haben:  
  
-   **Die Onlinekontos** ? Wenn Sie verhindern, dass einen Benutzer mithilfe von Office365 ohne Zugriff auf Ressourcen auf dem Server verhindern möchten, sollten Sie das Onlinekonto Zuweisung aufheben. Die Office365--Lizenz wird freigegeben ist, und des Benutzers mit Office365 anmelden. Der Server behält jedoch die Zuordnung zwischen den Namen des Benutzerkontos und der Office365 E-Mail-Adresse. Anweisungen finden Sie unter [Aufheben der Zuweisung ein Onlinekontos von einem Benutzerkonto](#BKMK_ToUnassignAnOnlineAccount).  
  
-   **Deaktivieren Sie das Benutzerkonto** ? Wenn Sie ein Benutzerkonto deaktivieren, da ein Mitarbeiter vorübergehend oder dauerhaft verlässt wird das Onlinekonto des Benutzers s ebenfalls deaktiviert. Das Onlinekonto kann nicht verwendet werden, aber die Benutzerdaten, einschließlich der E-Mails, bleiben in Microsoft Online Services. Anweisungen finden Sie unter [deaktivieren ein Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) in [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
-   **Entfernen Sie das Benutzerkonto** ? Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls aus Microsoft Online Services entfernt. Anweisungen finden Sie unter [Entfernen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) in [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
    > [!WARNING]
    >  Beachten Sie, dass wenn ein Onlinekonto entfernt wird, die Benutzerdaten unterliegen den Datenaufbewahrungsrichtlinien von Microsoft Online Services. Wenn Sie müssen die Benutzerdaten der Person s beibehalten, nachdem ein Mitarbeiter das Unternehmen verlässt, deaktivieren Sie das Benutzerkonto statt es zu entfernen.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a>Aufheben der Zuweisung ein Onlinekontos von einem Benutzerkonto  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Zuweisung ein Microsoft Onlinekontos** (in Windows Server Essentials, klicken Sie auf **Zuweisung ein Office365-Kontos**).  
  
3.  Klicken Sie bei der bestätigungsaufforderung auf **Ja**.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a>Verwalten von E-Mail-Adressen für Exchange Online  
 E-Mail-Adressen zu den Online-s-Benutzerkonto in Windows Server Essentials hinzufügen, können Sie dem Benutzer, E-Mails über mehrere E-Mail-Adressen in Exchange Online erhalten ermöglichen.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a>So fügen zusätzliche E-Mail-Adressen für einen Benutzer s Microsoft Onlinekonto  
  
1.  Klicken Sie auf dem Windows Server Essentials-Dashboard auf **Benutzer**.  
  
2.  Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Auf der **Microsoft online** in den Kontoeigenschaften auf der Registerkarte (oder die **Office365** Registerkarte in Windows Server Essentials), klicken Sie auf **hinzufügen**.  
  
4.  Geben Sie den neuen E-Mail-Alias ein, und wählen Sie dann die E-Mail-Domäne.  
  
5.  Klicken Sie auf **OK** zweimal.  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a>Verwalten von Verteilergruppen für Exchange Online (nur Windows Server Essentials)  
 Nachdem Sie Ihre Windows Server Essentials-Server mit Office365 integrieren, können Sie das Erstellen und Verwalten von Verteilergruppen für Exchange Online über das Windows Server Essentials-Dashboard. Alles Sie dazu die **Verteilergruppen** Registerkarte, die hinzugefügt werden, die **Benutzer** Seite. Diese Registerkarte wird nur angezeigt, wenn Sie ein Exchange Online-Abonnement verfügen. Dieses Feature ist nicht verfügbar in Windows Server Essentials.  
  
 Verwenden Sie die folgenden Verfahren, um:  
  
-   [Hinzufügen einer Verteilergruppe](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [Ändern der Mitglieder einer Verteilergruppe](#BKMK_ChangeGroupMembers)  
  
-   [Ändern Sie eine Verteilung s Gruppenmitgliedschaften](#BKMK_EditUserMemberships)  
  
-   [Entfernen von Verteilergruppen](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a>So fügen Sie eine Verteilergruppe hinzu  
  
1.  Klicken Sie auf die in Windows Server Essentials-Dashboard auf **Benutzer**, und klicken Sie dann auf die **Verteilergruppen** Registerkarte.  
  
2.  In **Verteilergruppenaufgaben**, klicken Sie auf **eine Verteilergruppe hinzufügen**.  
  
     Hinzufügen, wird ein Assistent für neue Verteilungspunkte Gruppe angezeigt.  
  
3.  Auf der **Hinzufügen einer neuen Verteilergruppe** Seite, geben Sie die folgenden Informationen ein, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie einen Gruppennamen, die optional eine Beschreibung und die E-Mail-Alias für die neue Verteilergruppe ein.  
  
    -   Standardmäßig kann die Verteilergruppe E-Mails von Personen außerhalb Ihrer Organisation erhalten. Wenn Sie nicht, um dies zu ermöglichen möchten, deaktivieren Sie diese Option.  
  
4.  Auf der **Gruppenmitglieder hinzufügen** Seite, verwenden Sie die **hinzufügen** um aktive Benutzerkonten hinzufügen, die ein Onlinekonto zugewiesen haben und andere Verteilergruppen zur neuen Verteilergruppe. Klicken Sie dann auf **Weiter**.  
  
     Die neue Verteilergruppe wird in Exchange Online erstellt werden.  
  
###  <a name="BKMK_ChangeGroupMembers"></a>So ändern Sie die Mitglieder einer Verteilergruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**, und klicken Sie dann auf die **Verteilergruppen** Registerkarte.  
  
2.  Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **Ändern der Gruppenmitgliedschaft**.  
  
3.  Verwenden der **hinzufügen** und **entfernen** Schaltflächen hinzufügen oder entfernen aktive Onlinekonten zur Verteilergruppe. Klicken Sie dann auf **Weiter** die Verteilergruppenmitgliedschaft in Exchange Online zu aktualisieren.  
  
###  <a name="BKMK_EditUserMemberships"></a>So ändern Sie einen Benutzer s Verteilergruppenmitgliedschaften  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Klicken Sie in den Eigenschaften des Benutzerkontos, auf die **Verteilergruppen** Registerkarte, und klicken Sie dann auf **bearbeiten**.  
  
4.  In der **Gruppenmitgliedschaft bearbeiten**, verwenden die **hinzufügen** und **entfernen** Schaltflächen zum Hinzufügen oder Entfernen von Verteilergruppen über das Benutzerkonto, und klicken Sie dann auf **schließen**.  
  
5.  Klicken Sie auf **OK** an die aktualisierten Benutzerkontoeigenschaften zu speichern.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a>So entfernen Sie eine Verteilergruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**, und klicken Sie dann auf die **Verteilergruppen** Registerkarte.  
  
2.  Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **entfernen Sie die Gruppe**.  
  
3.  Klicken Sie bei der bestätigungsaufforderung auf **Gruppe löschen**.  
  
     Die Verteilergruppe wird aus Exchange Online entfernt.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Office365](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
