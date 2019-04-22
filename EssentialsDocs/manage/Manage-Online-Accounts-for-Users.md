---
title: Verwalten von Online-Konten für Benutzer von Windows Server Essentials
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824091"
---
# <a name="manage-online-accounts-for-windows-server-essentials-users"></a>Verwalten von Online-Konten für Benutzer von Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie Ihre Windows Server Essentials-Server mit Microsoft Office 365 integrieren, können Sie Ihre Onlinekonten und Benutzerkonten über das Dashboard verwalten. In diesem Thema Sie ll herausfinden, welche Vorteile Sie durch die Verwaltung Ihrer Benutzer Microsoft Online Services-Konten über das Dashboard, das Erstellen und Verwalten von Onlinekonten über das Dashboard, und so verwalten Sie e-Mail-Adressen und Verteilergruppen für Exchange Online über das Dashboard.  

  
> [!NOTE]
>  Um Ihre Microsoft Online Services-Konten in Windows Server Essentials verwalten zu können, müssen Sie Ihren Server mit Office 365 integrieren. Anweisungen hierzu finden Sie unter [Verwalten von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md).  
  
> [!IMPORTANT]
>  Wenn Sie Onlinekonten in Windows Server Essentials verwalten, Sie daran gewöhnt, dass Microsoft Online Services-Konten als *Office 365-Konten*. Auf dem Dashboard in Windows Server Essentials-Bezeichnungen wurden geändert, um *Microsoft Online Services-Konten*, oder *Microsoft-Onlinekonten* kurz. Die Konten und die Verfahren sind identisch. Nur die Bezeichnungen wurden geändert. In den meisten Verfahren in diesem Thema wird der Begriff *Onlinekonto*verwendet.  
  
## <a name="in-this-topic"></a>Inhalt dieses Themas  
  
-   [Warum sollte ich meine Onlinekonten über das Dashboard verwalten?](#BKMK_WhyManageOnlineAccounts)  
  
-   [Erstellen von Onlinekonten](#BKMK_SECTION_CreateOnlineAccounts)  
  
-   [Verwalten von Onlinekonten](#BKMK_SECTION_ManageOnlineAccounts)  
  
-   [Verwalten von e-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses)  
  
-   [Verwalten von Verteilergruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups)  
  
##  <a name="BKMK_WhyManageOnlineAccounts"></a> Warum sollte ich meine Onlinekonten über das Dashboard verwalten?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, die Kennwörter der werden automatisch synchronisiert, und Sie die beiden Konten gemeinsam während des Benutzer-Konto-s-Lebenszyklus verwalten können.  
  
 Es s, die für den Benutzer bereit, die das gleiche Kennwort zum Zugriff auf Ressourcen auf dem Server und in Office 365 verwenden kann. Und Sie können die gleichen kennwortanforderungen für den Zugriff auf Ressourcen in Office 365, die Sie für internen Ressourcen benötigen anwenden.  
  
### <a name="how-does-password-synchronization-work"></a>Wie funktioniert die Kennwortsynchronisierung?  
 Wenn Sie das Dashboard verwenden, um ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, wird das Kennwort des Benutzerkontos automatisch mit dem Onlinekonto des Benutzers s synchronisiert. Dies bedeutet, dass ein Benutzer nur Zugriff auf die Ressourcen auf dem Server und Office 365 ein einziges Kennwort benötigt. Darüber hinaus können Sie den gleichen Namen für das Benutzerkonto und die Benutzer s-online-ID verwenden.  
  
 Die Kennwortsynchronisierung erfolgt umgehend und automatisch, wenn ein Benutzer das Kennwort für das Benutzerkonto auf einem zur Domäne gehörigen Computer oder mithilfe von Remotewebzugriff ändert.  
  
> [!IMPORTANT]
>  Wenn Office 365 mit Windows Server Essentials integriert ist, sollten Benutzer das Kennwort für ihr Microsoft Onlinekonto aus dem Office 365-Portal nicht ändern. Auf diese Weise wird die Kennwortsynchronisierung unterbrochen.  
  
### <a name="simplified-account-creation"></a>Vereinfachte Kontoerstellung  
 Dort s ein weiterer Vorteil bei der Erstellung der ursprünglichen Onlinekonten über das Dashboard. Sie können Onlinekonten für alle Benutzer mit einer einzelnen Aktion erstellen. Auf der anderen Seite können, wenn Ihre Mitarbeiter Office 365 bereits verwenden, und Sie einen neuen Windows Server Essentials-Server einrichten, Sie alle Ihre Benutzerkonten aus den Onlinekonten, mit einer einzelnen Aktion erstellen. Weitere Informationen finden Sie unter [Erstellen von Onlinekonten](#BKMK_SECTION_CreateOnlineAccounts).  
  
### <a name="manage-email-addresses-and-distribution-groups-from-the-dashboard"></a>Verwalten von E-Mail-Adressen und Verteilergruppen über das Dashboard  
 Sie können E-Mail-Adressen und Verteilergruppen für Exchange Online über das Dashboard verwalten. Und Sie können Ihre Organisation s Internetdomäne die e-Mail-Adressen verwenden. Sie können all dies über das Dashboard durchführen, ohne Anmeldung bei Office 365. (Sie müssen Sie Windows Server Essentials verwenden werden, um Verteilergruppen über das Dashboard verwalten. Dieses Feature wird nicht in Windows Server Essentials unterstützt.) Weitere Informationen finden Sie unter [Verwalten von E-Mail-Adressen für Exchange Online](#BKMK_SECTION_ManageEmailAddresses) und [Verwalten von Verteilergruppen für Exchange Online](#BKMK_SECTION_ManageDistributionGroups).  
  
### <a name="manage-the-user-account-and-online-account-together"></a>Gemeinsames Verwalten von Benutzerkonto und Onlinekonto  
 Und Sie können Onlinekonten zusammen mit das Benutzerkonto, das während des Lebenszyklus des Kontos s verwalten. Wenn Sie das Benutzerkonto deaktivieren, wird das Onlinekonto in Microsoft Online Services ebenfalls deaktiviert. Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls entfernt. Weitere Informationen finden Sie unter [Verwalten von Onlinekonten](#BKMK_SECTION_ManageOnlineAccounts).  
  
##  <a name="BKMK_SECTION_CreateOnlineAccounts"></a> Erstellen von Onlinekonten  
 Nachdem Sie Ihre Server mit Office 365 integrieren sie s von Vorteil, erstellen Sie Microsoft Online Services-Konten für Ihre Benutzer über das Dashboard. Sie haben ein hohes Maß an Flexibilität bei der Erstellung der Onlinekonten. Wenn Sie ein neues Office 365-Abonnement verfügen, können Sie Bulk Onlinekonten für alle Benutzer erstellen. Wenn Sie bereits Onlinekonten in Office 365 erstellt haben, Einbau zusätzlichen Sie Sorge. Wenn Sie einen neuen Server einrichten, Sie Ihre Benutzerkonten auf dem Server erstellen können, indem Sie die Onlinekonten importieren. Und Sie können ein neues oder ein vorhandenes Onlinekonto zuweisen, wenn Sie ein einzelnes Benutzerkonto erstellen oder wenn Sie ein online-Konto zu einem vorhandenen Benutzerkonto hinzufügen.  
  
 **Lizenzanforderungen** Sie benötigen eine Benutzerlizenz für alle Onlinekonten, die Sie erstellen. Überprüfen Sie die **Office 365** -Seite des Dashboards angezeigt, wie viele Benutzerlizenzen über Ihr Office 365-Abonnement zur Verfügung stehen. Bei Bedarf weitere Lizenzen für Benutzer hinzufügen, werden Sie ll Ihres Office 365-Abonnements in Office 365, um dies zu öffnen.  
  
 **Anschlussmaßnahme für Benutzer** Nachdem Sie ein Onlinekonto für ein Benutzerkonto hinzugefügt haben, ist der Benutzer das Kennwort für ihr Benutzerkonto der nächsten Anmeldung ändern seiner Anmeldung erforderlich. Das neue Kennwort wird sofort mit dem Onlinekonto synchronisiert. Danach können sie das Kennwort verwenden, zur Anmeldung beim Office 365 mit ihrer online-ID  
  
> [!IMPORTANT]
>  Betonen Sie Ihre Benutzer, dass sie ihre online-Konto-Kennworts in Office 365 nie ändern sollten. Das Kennwort wird immer dann automatisch geändert, wenn sie das Kennwort für ihr Benutzerkonto ändern. Wenn sie das onlinekennwort in Office 365 ändern, wird die kennwortsynchronisierung unterbrochen werden.  
  
 Verwenden Sie die Verfahren in diesem Abschnitt für Folgendes:  
  
-   [Erstellen Sie Onlinekonten für vorhandene Benutzerkonten per Massenimport](#BKMK_ToBulkCreateOnlineAccounts)  
  
-   [Importieren Sie Benutzerkonten aus Ihrer Microsoft Online Services-Konten](#BKMK_ToImportUserAccounts)  
  
-   [Erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto](#BKMK_ToCreateaNewUserAccount)  
  
-   [Zuweisen eines Onlinekontos zu einem Benutzerkonto](#BKMK_ToAssignAnOnlineAccount)  
  
> [!NOTE]
>  Wenn Sie mit Windows Server Essentials, Sie sehen *Office 365-Konto* anstelle von *Microsoft Online Services-Konto* während dieses Vorgangs. Der Prozess ist identisch, aber die Terminologie ist anders in Windows Server Essentials.  
  
###  <a name="BKMK_ToBulkCreateOnlineAccounts"></a> Um die Onlinekonten für vorhandene Benutzerkonten per Massenimport erstellen  
  
1.  Melden Sie sich auf dem Server als Administrator, und öffnen Sie Windows Server Essentials-Dashboard.  
  
2.  Öffnen Sie auf dem Dashboard die Seite **Benutzer**.  
  
3.  Klicken Sie unter **Benutzeraufgaben** auf **Microsoft Onlinekonten hinzufügen**.  
  
     Die Seite **Microsoft Online Services-Konten hinzufügen** des Assistenten zeigt alle Benutzerkonten, die nicht über ein Microsoft Onlinekonto verfügen. Alle Konten sind standardmäßig ausgewählt, und der Benutzername wird für die Microsoft Online-ID empfohlen. Wenn Sie eine benutzerdefinierte Internetdomäne mit Ihrem Office 365-Abonnement verknüpft haben, wird standardmäßig diese Domäne verwendet werden.  
  
4.  Prüfen Sie auf der Seite **Microsoft Online Services-Konten hinzufügen** die Konten, die erstellt werden. Prüfen Sie z. B. auf Benutzer, die bereits ein Onlinekonto mit einer anderen Online-ID besitzen, und stellen Sie sicher, dass die Domäne, die Sie in E-Mail-Adressen verwenden möchten, ausgewählt ist. Wenn Sie alle erforderlichen Änderungen vorgenommen haben, klicken Sie auf **Weiter**.  
  
5.  Auf der **Zuweisen von Microsoft Online Services-Lizenzen** Seite, auf Office 365-Dienste, die Ihre Benutzer verwenden. Wenn Sie auf **Weiter** klicken, wird die Kontoerstellung gestartet.  
  
    > [!NOTE]
    >  Sie müssen eine Service-Lizenz im Office 365 für jedes Onlinekonto sein. Sie können die verfügbaren Lizenzen überprüfen und können ggf. das Abonnement zum Hinzufügen von Lizenzen von der **Office 365** -Seite des Dashboards öffnen.  
  
6.  Benachrichtigen Sie die Benutzer, dass sie nun über ein Microsoft Onlinekonto verfügen. Sie müssen das Kennwort für ihr Netzwerk ändern, bevor sie mit Office 365 anmelden können. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
###  <a name="BKMK_ToBeginUsingAnOnlineAccount"></a> Erste Schritte mit dem neuen Microsoft Onlinekonto  
  
1.  Melden Sie sich auf dem Computer mit dem Netzwerkbenutzerkonto an.  
  
2.  Ändern Sie das Kennwort für das Benutzerkonto. Drücken Sie zuerst STRG+ALT+ENTF, und klicken Sie dann auf **Kennwort ändern**.  
  
     Wenn Sie Ihr Kennwort ändern, wird das Kennwort mit dem neuen Onlinekonto synchronisiert. Sie können nun das gleiche Kennwort verwenden, zur Anmeldung beim Office 365.  
  
3.  [Melden Sie sich bei Office 365](https://login.microsoftonline.com/login.srf?wa=wsignin1.0&rpsnv=3&ct=1398981834&rver=6.1.6206.0&wp=MBI_SSL&wreply=https:%2F%2Foutlook.office365.com%2Fowa%2F&id=260563&CBCXT=out) mit Ihrer neuen Online-ID und dem Kennwort Ihres Benutzerkontos an.  
  
    > [!IMPORTANT]
    >  Ändern Sie das Kennwort Ihres Onlinekontos in Office 365 nicht. Auf diese Weise wird die Kennwortsynchronisierung unterbrochen. Ihr Onlinekennwort wird jedes Mal aktualisiert, wenn Sie das Kennwort für das Netzwerkbenutzerkonto ändern.  
  
###  <a name="BKMK_ToImportUserAccounts"></a> So importieren Sie Benutzerkonten aus Ihren vorhandenen Onlinekonten  
  
1.  Öffnen Sie auf dem Dashboard die Seite **Benutzer**.  
  
2.  Klicken Sie unter **Benutzeraufgaben**auf **Konten aus Office 365 importieren**.  
  
     Die nächste Seite zeigt alle Onlinekonten für Ihr Office 365-Abonnement, die nicht über ein Benutzerkonto auf dem Server verfügen. Alle Konten sind standardmäßig ausgewählt, und die Online-ID wird als Benutzername vorgeschlagen.  
  
3.  So erstellen Sie die Benutzerkonten:  
  
    1.  Nehmen Sie alle erforderlichen Änderungen an den vorgeschlagenen Benutzerkonten vor.  
  
    2.  Klicken Sie optional auf den Link, um die temporären Kennwörter anzuzeigen, die den Benutzerkonten zugewiesen werden. Sie müssen den Benutzern ihre temporären Kennwörter zusammen mit ihren neuen Kontonamen mitteilen.  
  
         (Nachdem Sie die Konten erstellt haben, Sie finden diese Kennwörter in dieser Datei aufgeführt: *Systemlaufwerk*\Users\\*Office365admin*\\*NewServerUser*txt, in denen *Office365admin* ist das Netzwerkzugriffskonto Dient zum Verwalten von Office 365 auf dem Server und *NewServerUser* ist der Name des neuen Benutzerkontos.)  
  
    3.  Klicken Sie auf **Weiter** , um die Benutzerkonten zu erstellen.  
  
4.  Lassen Sie Ihre Benutzer ihre neue Benutzerkonten sowie die temporären Kennwörter, verwenden sie für die Anmeldung auf dem Server für das erste Mal œ und, die das Kennwort zu ändern, nachdem sie sich anmelden müssen. Anweisungen finden Ihre Benutzer unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
     Achten Sie darauf, dass sie wissen, dass die Kennwörter für ihr Onlinekonto mit ihrem Benutzerkonto, das in Zukunft synchronisiert werden, und sie sollten ihr onlinekennwort in Office 365 nicht ändern.  
  
###  <a name="BKMK_ToCreateaNewUserAccount"></a> Erstellen Sie ein neues Benutzerkonto mit einem zugewiesenen Onlinekonto  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie unter **Benutzeraufgaben**auf **Benutzerkonto hinzufügen**. Der Assistent für das Hinzufügen eines Benutzerkontos wird angezeigt.  
  
3.  Folgen Sie den Anweisungen, um das Benutzerkonto zu erstellen.  
  
4.  Erstellen Sie auf der Seite **Ein Microsoft Online Services-Konto zuweisen** entweder ein neues Onlinekonto für den Benutzer oder weisen Sie ein vorhandenes Onlinekonto zu:  
  
    -   Klicken Sie zum Erstellen eines neuen Onlinekontos auf **Ein neues Microsoft Online Services-Konto erstellen und diesem Benutzerkonto zuweisen**, und geben Sie einen Namen für das Microsoft Online Services-Konto ein. (Standardmäßig wird der Benutzername für die Online-ID verwendet.) Klicken Sie dann auf **Weiter**.  
  
    -   Klicken Sie auf **Ein vorhandenes Microsoft Online Services-Konto diesem Benutzerkonto zuweisen**, um ein vorhandenes Microsoft Onlinekonto zuzuweisen, und wählen Sie ein vorhandenes Konto aus der Dropdownliste aus. Klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]
    >  Microsoft Online Services-Konten werden in Windows Server Essentials als Office 365-Konten im Assistenten und Dashboard bezeichnet.  
  
5.  Folgen Sie den Anweisungen, um den Assistenten fertigzustellen.  
  
6.  Benachrichtigen Sie den Benutzer, dass er das Kennwort des Benutzerkontos ändern muss, bevor er sich bei Office 365 mit dem neuen Onlinekonto anmelden kann. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
#### <a name="BKMK_ToAssignAnOnlineAccount"></a>Ein online-Konto einem Benutzerkonto zuweisen  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Ein Microsoft Onlinekonto zuweisen**. Der Assistent für die Zuweisung eines Microsoft Online Services-Kontos wird angezeigt.  
  
3.  Weisen Sie ein vorhandenes Onlinekonto zu, oder erstellen Sie ein neues für den Benutzer. Die Standard-Online-ID für ein neues Konto ist der Benutzername. Klicken Sie dann auf **Weiter** , um das Onlinekonto dem Benutzerkonto hinzuzufügen.  
  
4.  Überprüfen Sie die Informationen auf der letzten Seite des Assistenten, und klicken Sie dann auf **Schließen**.  
  
5.  Benachrichtigen Sie den Benutzer, dass er das Kennwort des Benutzerkontos ändern muss, bevor er sich bei Office 365 mit dem neuen Onlinekonto anmelden kann. Anweisungen finden Sie unter [Erste Schritte mit dem neuen Microsoft Onlinekonto](#BKMK_ToBeginUsingAnOnlineAccount).  
  
##  <a name="BKMK_SECTION_ManageOnlineAccounts"></a> Verwalten von Onlinekonten  
 Wenn Sie ein Benutzerkonto in Windows Server Essentials ein Onlinekonto hinzufügen, können Sie beide Konten während des kontolebenszyklus s zusammen verwalten.  
  
###  <a name="BKMK_UnderstandingAccountStatus"></a> Grundlegendes zu den Status online-Konto  
 Wenn Sie ein Microsoft Online Services-Konto einem Benutzerkonto zuweisen, wird die E-Mail-Adresse für das Konto in der **Microsoft Onlinekonto**-Spalte auf der Seite **Benutzer** des Dashboards angezeigt. (In Windows Server Essentials ist die Bezeichnung der Spalte **Office 365-Konto**.)  
  
-   Ein blaues Symbol neben einer E-Mail-Adresse gibt an, dass das Onlinekonto aktiv ist. D. h. das Konto über eine aktuelle Office 365-Lizenz verfügt, und der Benutzer kann die online-ID für die Anmeldung bei Office 365 verwenden.  
  
-   Ein schattiertes Symbol neben der e-Mail-Adresse gibt an, das online-Konto ist entweder inaktiv œ, weil die Lizenz nicht mehr aktiv ist oder das Onlinekonto nicht zugewiesen wurde. Wenn Sie ein Onlinekonto des Benutzers s Zuweisung aufgehoben werden, die Lizenz entfernt, und der Benutzer, die Anmeldung bei Office 365 über das Konto gesperrt ist. Der Server behält jedoch die Zuordnung zwischen den Namen des Benutzerkontos und der Office 365-e-Mail-Adresse.  
  
###  <a name="BKMK_UnassignOnlineAccount"></a> Beschränken des Zugriffs auf ein online-Konto  
 Was tun Sie, wenn ein Benutzer die Organisation verlässt oder Sie die Benutzer-s-Zugriff auf Ihre Office 365-Dienste einschränken möchten? Wenn Sie Ihren Benutzern Onlinekonten zusammen mit den Benutzerkonten in Windows Server Essentials verwalten, Ihnen drei Optionen zur Verfügung:  
  
-   **Onlinekontos** ? Wenn Sie verhindern, dass einen Benutzer mit Office 365 ohne Zugriff auf Ressourcen auf dem Server verhindern möchten, sollten Sie das online-Konto Zuweisung aufheben. Die Office 365-Lizenz wird freigegeben, und der Benutzer die Anmeldung bei Office 365 gesperrt ist. Der Server behält jedoch die Zuordnung zwischen den Namen des Benutzerkontos und der Office 365-e-Mail-Adresse. Anweisungen hierzu finden Sie unter [, die von einem Benutzerkonto Onlinekonten](#BKMK_ToUnassignAnOnlineAccount).  
  
-   **Deaktivieren Sie das Benutzerkonto** ? Wenn Sie ein Benutzerkonto deaktivieren, da ein Mitarbeiter vorübergehend oder dauerhaft, verlässt, ist das Onlinekonto des Benutzers s ebenfalls deaktiviert. Das Onlinekonto kann nicht verwendet werden, aber die Benutzerdaten, einschließlich E-Mails, werden in Microsoft Online Services beibehalten. Anweisungen hierzu finden Sie unter [Deaktivieren von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage6) in [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
-   **Entfernen des Benutzerkontos** ? Wenn Sie ein Benutzerkonto entfernen, wird das Onlinekonto ebenfalls aus Microsoft Online Services entfernt. Anweisungen hierzu finden Sie unter [Entfernen eines Benutzerkontos](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Remove) in [Manage User Accounts](Manage-User-Accounts-in-Windows-Server-Essentials.md).  
  
    > [!WARNING]
    >  Beachten Sie, dass bei einer Entfernung eines Onlinekontos die Benutzerdaten den Datenaufbewahrungsrichtlinien von Microsoft Online Services unterliegen. Wenn Sie müssen die Person-s-Benutzerdaten beibehalten werden sollen, nachdem ein Mitarbeiter verlässt, deaktivieren Sie das Benutzerkonto, anstatt es zu entfernen.  
  
####  <a name="BKMK_ToUnassignAnOnlineAccount"></a> Beim Aufheben der Zuweisung einer online-Konto von einem Benutzerkonto  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Mit der rechten Maustaste in des Benutzerkontos in der Liste aus, und klicken Sie dann auf **Zuweisung ein Microsoft Onlinekontos** (klicken Sie in Windows Server Essentials auf **Zuweisung von Office 365-Konto**).  
  
3.  Klicken Sie bei der Bestätigungsaufforderung auf **Ja**.  
  
##  <a name="BKMK_SECTION_ManageEmailAddresses"></a> Verwalten von e-Mail-Adressen für Exchange Online  
 Durch die Benutzer s-online-Konto in Windows Server Essentials-e-Mail-Adressen hinzugefügt haben, können Sie zulassen, dass der Benutzer, e-Mails über mehrere e-Mail-Adressen in Exchange Online zu erhalten.  
  
###  <a name="BKMK_PROC_AddEmailAliases"></a> Zusätzliche e-Mail-Adressen zu einem Benutzer s Microsoft online-Konto hinzufügen  
  
1.  Klicken Sie auf der Windows Server Essentials-Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Auf der **Microsoft online** den Kontoeigenschaften auf der Registerkarte (oder die **Office 365** Registerkarte in Windows Server Essentials), klicken Sie auf **hinzufügen**.  
  
4.  Geben Sie den neuen E-Mail-Alias ein, und wählen Sie dann die E-Mail-Domäne aus.  
  
5.  Klicken Sie zweimal auf **OK** .  
  
##  <a name="BKMK_SECTION_ManageDistributionGroups"></a> Verwalten von Verteilergruppen für Exchange Online (nur Windows Server Essentials)  
 Nachdem Sie Ihre Windows Server Essentials-Server in Office 365 integrieren, können Sie erstellen und Verwalten von Verteilergruppen für Exchange Online über das Windows Server Essentials-Dashboard. Sie ll dazu die **Verteilergruppen** Registerkarte, die hinzugefügt wird, die **Benutzer** Seite. Diese Registerkarte wird nur angezeigt, wenn Sie über ein Exchange Online-Abonnement verfügen. Dieses Feature ist nicht in Windows Server Essentials verfügbar.  
  
 Verwenden Sie die folgenden Verfahren für Folgendes:  
  
-   [Eine Verteilergruppe hinzufügen](#BKMK_PROCEDURE_AddDistGroup)  
  
-   [Ändern der Mitglieder einer Verteilergruppe](#BKMK_ChangeGroupMembers)  
  
-   [Ändern Sie eine Benutzer-s-Verteilergruppenmitgliedschaften](#BKMK_EditUserMemberships)  
  
-   [Entfernen von Verteilergruppen](#BKMK_RemoveDistributionGroup)  
  
###  <a name="BKMK_PROCEDURE_AddDistGroup"></a> Eine Verteilergruppe hinzufügen  
  
1.  Klicken Sie auf die in Windows Server Essentials-Dashboard auf **Benutzer**, und klicken Sie dann auf die **Verteilergruppen** Registerkarte.  
  
2.  Klicken Sie unter **Verteilergruppenaufgaben**auf **Eine Verteilergruppe hinzufügen**.  
  
     Der Assistent für das Hinzufügen einer neuen Verteilergruppe wird angezeigt.  
  
3.  Geben Sie die folgenden Informationen auf der Seite **Eine neue Verteilergruppe hinzufügen** ein, und klicken Sie dann auf **Weiter**:  
  
    -   Geben Sie einen Gruppennamen, die Beschreibung und den E-Mail-Alias für die neue Verteilergruppe ein.  
  
    -   Standardmäßig kann die Verteilergruppe E-Mails von Personen außerhalb Ihrer Organisation empfangen. Wenn dies nicht möglich sein soll, deaktivieren Sie diese Option.  
  
4.  Verwenden Sie auf der Seite **Gruppenmitglieder hinzufügen** die Schaltfläche **Hinzufügen**, um aktive Benutzerkonten, denen ein Onlinekonto zugewiesen wurde, und andere Verteilergruppen zur neuen Verteilergruppe hinzuzufügen. Klicken Sie dann auf **Weiter**.  
  
     In Exchange Online wird die neue Verteilergruppe erstellt.  
  
###  <a name="BKMK_ChangeGroupMembers"></a> So ändern Sie die Mitglieder einer Verteilergruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**und dann auf die Registerkarte **Verteilergruppen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **Ändern der Gruppenmitgliedschaft**.  
  
3.  Verwenden Sie die Schaltflächen **Hinzufügen** und **Entfernen** , um aktive Onlinekonten zur Verteilergruppe hinzuzufügen oder daraus zu entfernen. Klicken Sie dann auf **Weiter**, um die Verteilergruppenmitgliedschaft in Exchange Online zu aktualisieren.  
  
###  <a name="BKMK_EditUserMemberships"></a> So ändern Sie einen Benutzer s Verteilergruppenmitgliedschaften  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto in der Liste, und klicken Sie dann auf **Kontoeigenschaften anzeigen**.  
  
3.  Klicken Sie in den Eigenschaften des Benutzerkontos auf die Registerkarte **Verteilergruppen**, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Verwenden Sie im Feld **Gruppenmitgliedschaft bearbeiten** die Schaltflächen **Hinzufügen** und **Entfernen** , um Verteilergruppen zum Benutzerkonto hinzuzufügen oder daraus zu entfernen, und klicken Sie dann auf **Schließen**.  
  
5.  Klicken Sie auf **OK**, um die aktualisierten Benutzerkontoeigenschaften zu speichern.  
  
###  <a name="BKMK_RemoveDistributionGroup"></a> So entfernen Sie eine Verteilergruppe  
  
1.  Klicken Sie auf dem Dashboard auf **Benutzer**und dann auf die Registerkarte **Verteilergruppen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Verteilergruppe in der Liste, und klicken Sie dann auf **Gruppe entfernen**.  
  
3.  Klicken Sie bei der Bestätigungsaufforderung auf **Gruppe löschen**.  
  
     Die Verteilergruppe wird aus Exchange Online entfernt.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwalten von Benutzerkonten](Manage-User-Accounts-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Office 365](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
