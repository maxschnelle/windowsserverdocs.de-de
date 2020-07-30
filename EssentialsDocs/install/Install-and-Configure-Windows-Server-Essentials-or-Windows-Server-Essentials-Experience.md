---
title: Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 804a3ed902606e52f25977601e4edc2e2fc5e04f
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181186"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials ist ein idealer erster Server für kleine Unternehmen mit bis zu 25 Benutzern und 50 Geräten. Für Organisationen mit bis zu 100 Benutzern und 200 Geräten können Sie nun Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle verwenden. Dieses Thema zielt auf beide Szenarien ab.

Windows Server Essentials ist eine Rolle in Windows Server 2016, mit der Sie alle Features (z. b. Remote Webzugriff und PC-Sicherung) nutzen können, die für Sie in Windows Server Essentials verfügbar sind, ohne dass die Sperren und Einschränkungen in Windows Server Essentials erzwungen werden. Diese Server Rolle ist auch in Windows Server Essentials verfügbar und standardmäßig aktiviert.

Beachten Sie vor der Installation von Windows Server Essentials oder der Essentials-Benutzerrolle die folgenden Einschränkungen.

|Windows Server Essentials-Darstellung in Windows Server Essentials|Windows Server Essentials-Darstellung in Windows Server 2016
|----|----|
|-Muss der Domänen Controller im Stamm der Gesamtstruktur und Domäne sein und muss alle FSMO-Rollen enthalten.<br /><br /> -Kann nicht in einer Umgebung mit einer bereits vorhandenen Active Directory Domäne installiert werden (es gibt jedoch eine Karenzzeit von 21 Tagen für die Durchführung von Migrationen).|-Muss kein Domänen Controller sein, wenn er in einer Umgebung mit einer bereits vorhandenen Active Directory Domäne installiert ist.<br /><br /> Wenn eine Active Directory Domäne nicht vorhanden ist, wird durch die Installation der Rolle eine Active Directory Domäne erstellt, und der Server wird zum Domänen Controller im Stamm der Gesamtstruktur und Domäne, in der alle FSMO-Rollen enthalten sind.
|Kann nur in einer einzelnen Domäne bereitgestellt werden.|Kann nur in einer einzelnen Domäne bereitgestellt werden.
|In Ihrer Domäne darf kein schreibgeschützter Domänencontroller vorhanden sein.|In Ihrer Domäne darf kein schreibgeschützter Domänencontroller vorhanden sein.

> [!NOTE]
>  Besuchen Sie zum Herunterladen von Evaluierungsversionen des Betriebssystems das TechNet Evaluierungscenter :
>
>  [Herunterladen von Windows Server 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)
>
>  [Herunterladen von Windows Server Essentials](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)

## <a name="installation-options"></a>Installationsoptionen
 Dieses Dokument enthält schrittweise Anleitungen zum Installieren und Konfigurieren von Windows Server Essentials. In Abhängigkeit Ihrer Netzwerkumgebung stehen Ihnen die folgenden Installationsoptionen zur Verfügung:

-    Windows Server Essentials (mit standardmäßig aktivierter Windows Server Essentials-Rolle)

-    Windows Server 2016 mit installierter Windows Server Essentials-Rolle

|Bereitstellungsumgebung|BESCHREIBUNG|Zugehöriger Abschnitt|
|----------------------------|-----------------|---------------------|
|Neue Active Directory-Umgebung|Sie können Windows Server Essentials zum Erstellen einer neuen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|
|Vorhandene Active Directory-Umgebung|Sie können Windows Server Essentials in einer vorhandenen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|
|Virtuelle Umgebung|Sie können Windows Server Essentials als virtuellen Computer bereitstellen.|[Virtualisieren Ihrer Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|
|Automatisierte Bereitstellung|Sie können die Bereitstellung von Windows Server Essentials mithilfe der Windows PowerShell automatisieren.|[Installieren und Konfigurieren von Windows Server Essentials mithilfe der Windows PowerShell](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|

## <a name="before-you-begin"></a>Voraussetzungen
 Lesen Sie vor dem Installieren die folgende Dokumentation:

-   [Windows Server Essentials – Produktübersicht](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)


-   [Systemanforderungen für Windows Server Essentials](../get-started/system-requirements.md)


##  <a name="deploy-windows-server-essentials-to-set-up-a-new-active-directory-environment"></a><a name="BKMK_NewAD"></a>Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory Umgebung
 Windows Server Essentials bietet Ihnen die Möglichkeit, eine Active Directory-Umgebung und zugehörige Serverfeatures schnell einzurichten.

###  <a name="deploying-windows-server-essentials"></a><a name="BKMK_WSEDeploy"></a>Bereitstellen von Windows Server Essentials
 Wenn Sie Windows Server Essentials verwenden, ist die Windows Server Essentials-Funktion bereits aktiviert. Sie müssen jedoch einige Schritte abschließen, um Ihren Server zu konfigurieren.

##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>So konfigurieren Sie Windows Server Essentials auf einem physischen Server

1. Im Anschluss an die Windows-Startseite**** wird der Assistent für die Konfiguration von Windows Server Essentials**** auf Ihrem Desktop angezeigt.

2. Befolgen Sie die Anweisungen, um den Assistenten wie folgt abzuschließen:

   1.  Klicken Sie auf der Seite **Windows Server Essentials konfigurieren** auf **Weiter**.

   2.  Stellen Sie unter **Uhrzeiteinstellungen** sicher, dass Datum, Uhrzeit und Zeitzone richtig sind, und klicken Sie dann auf **Weiter**.

   3.  Geben Sie unter **Firmeninformationen** Ihren Unternehmensnamen wie **Contoso,Ltd.** ein, und klicken Sie dann auf **Weiter**. Optional können Sie den internen Domänennamen und den Servernamen ändern.

   4.  Geben Sie unter der Option zum Erstellen eines Netzwerkadministrators**** einen neuen Administratorkontonamen und ein -kennwort ein.

       > [!NOTE]
       >  Verwenden Sie nicht den bzw. das standardmäßige(n) **Administrator**-Kontonamen und -kennwort.

   5.  Klicken Sie auf **Konfigurieren**.

3. Während des Konfigurationsvorgangs wird der Server mehrfach neu gestartet, und Ihre Anmeldungen erfolgen automatisch, bis die Konfiguration abgeschlossen ist. Dieser Vorgang nimmt etwa 20 Minuten in Anspruch.

4. Klicken Sie auf dem Desktop auf das Dashboardsymbol, um das Serverdashboard zu starten. Schließen Sie auf der Startseite**** die Aufgaben **Erste Schritte** ab, die auf der Registerkarte **Einrichtung** aufgelistet sind.

   Nach Abschluss der Serverkonfiguration wird der Server, auf dem Windows Server Essentials ausgeführt wird, als Domänencontroller festgelegt.

###  <a name="deploying-the-windows-server-essentials-experience-role-in-windows-server-2012-r2-standard-and-datacenter"></a><a name="BKMK_DeployWSERole"></a>Bereitstellen der Rolle "Windows Server Essentials-Benutzer" in Windows Server 2012 R2 Standard und Datacenter
 Sie können Server-Manager verwenden, um die Windows Server Essentials-Benutzerrolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mithilfe des folgenden Verfahrens zu aktivieren und zu konfigurieren.

##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>So stellen Sie die Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 bereit

1.  Melden Sie sich an Ihrem Server als ein lokaler Administrator an.

2.  Öffnen Sie **Server-Manager**, und klicken Sie dann auf **Rollen und Features hinzufügen**.

3.  Wählen Sie in **Serverrollen auswählen** die Rolle **Windows Server Essentials Experience** aus. Klicken Sie im Dialogfeld auf **Features hinzufügen** und dann auf **Weiter**.

4.  Klicken Sie in **Features** auf **Weiter**.

5.  Prüfen Sie die Rollenbeschreibung **Windows Server Essentials Experience**, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf den Seiten, die darauf folgen, auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **Installieren**.

7.  Nachdem die Installation beendet wurde, sollte Windows Server Essentials in Server-Manager als Server Rolle aufgeführt werden.

8.  Klicken Sie im Bereich für die Kennzeichnungsbenachrichtigung im Server-Manager auf die Kennzeichnung, und klicken Sie dann auf **Windows Server Essentials konfigurieren**.

9. (Optional) Ändern Sie bei Bedarf den Servernamen.

    > [!IMPORTANT]
    >  Sie können den Servernamen nicht ändern, nachdem Sie Windows Server Essentials konfiguriert haben.


10. Befolgen Sie den Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt Bereitstellen von [Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) beschrieben.

10. Befolgen Sie den Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt Bereitstellen von [Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) beschrieben.


##  <a name="deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a><a name="BKMK_ExistingAD"></a>Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory Umgebung
 Sie können Windows Server Essentials auch bereitstellen, wenn Ihre Organisation bereits über eine vorhandene Active Directory-Umgebung verfügt. Zusätzlich können Sie sich entscheiden, ob Sie Windows Server Essentials als einen Domänencontroller bereitstellen möchten.

> [!IMPORTANT]
>  Diese Option ist nur verfügbar, wenn Sie die Windows Server Essentials-Benutzerrolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter bereitstellen.

#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>So stellen Sie Windows Server Essentials in einer vorhandenen Active Directory-Umgebung bereit

1.  (Optional) Ändern Sie bei Bedarf den Servernamen.

    > [!IMPORTANT]
    >  Sie können den Servernamen nicht ändern, nachdem Sie Windows Server Essentials konfiguriert haben.

2.  Verknüpfen Sie Ihren Server unter Windows Server Essentials wie folgt mit einer vorhandenen Domäne:

    1.  Wenn dieser Server als Domänencontroller fungieren soll, richten Sie den Server als einen Replikatdomänencontroller ein.

    2.  Wenn dieser Server nicht als Domänencontroller fungieren soll, verknüpfen Sie diesen Server mit Ihrer Domäne, indem Sie die systemeigenen Windows-Tools verwenden.

3.  Starten Sie Ihren Server neu, und melden Sie sich am Server als ein Domänenadministrator an.

4.  Öffnen Sie den Server-Manager, und klicken Sie dann auf **Rollen und Features hinzufügen**.

5.  Klicken Sie auf den folgenden Seiten auf **Weiter**.

6.  Wählen Sie in **Serverrollen auswählen** die Rolle **Windows Server Essentials Experience** aus. Klicken Sie im Dialogfeld auf **Features hinzufügen** und dann auf **Weiter**.

7.  Klicken Sie in **Features** auf **Weiter**.

8.  Prüfen Sie die Beschreibung **Windows Server Essentials Experience**, und klicken Sie dann auf **Weiter**.

9. Klicken Sie auf den Seiten, die darauf folgen, auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **Installieren**.

10. Nach Abschluss der Installation wird Windows Server Essentials in Server-Manager als Server Rolle aufgeführt.

11. Klicken Sie im Meldungsinfobereich im **Server-Manager** auf Flag, und dann auf **Windows Server Essentials konfigurieren**.

12. Folgen Sie dem Assistenten zum Konfigurieren von Windows Server Essentials. In Abhängigkeit Ihrer Active Directory-Konfiguration werden Sie informiert, ob Sie Windows Server Essentials auf einem Domänencontroller oder als ein Domänenmitglied konfigurieren. Klicken Sie auf **Konfigurieren**, um die Konfiguration zu beginnen. Die Konfiguration dauert ungefähr 10 Minuten.

##  <a name="virtualize-your-environment"></a><a name="BKMK_VirtualWSE"></a>Virtualisieren Ihrer Umgebung
  Windows Server Essentials, Windows Server 2012 R2 Standard und Windows Server 2012 R2 Datacenter können als virtuelle Computer ausgeführt werden. Sie können virtuelle Computer ausführen, indem Sie die Hyper-V-Verwaltungstools auf einem Server unter Hyper-V verwenden. Aus Lizenzierungs Perspektive ermöglicht Windows Server Essentials Ihnen, die Hyper-V-Rolle einzurichten und Ihre Umgebung zu virtualisieren. Die Lizenz ermöglicht Ihnen das Einrichten eines anderen Gast Betriebssystems, auf dem Windows Server Essentials ausgeführt wird. Abhängig von der Konfiguration Ihres Systemanbieters ermöglicht Windows Server Essentials die nahtlose Einrichtung einer virtualisierten Umgebung.

#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>So stellen Sie Windows Server Essentials als einen virtuellen Computer bereit

1.  Nach der Windows-Willkommensseite (abhängig von der Konfiguration Ihres Systemanbieters) **bietet die Seite** Vorbereitung eine Option zum Einrichten von Windows Server Essentials als eine virtuelle Instanz oder auf physischer Hardware. Die Verfügbarkeit dieser Optionen wird durch Ihren Systemanbieter vorab definiert, und beide Optionen sind möglicherweise nicht immer verfügbar. Wenn Sie Windows Server Essentials als virtuellen Computer installieren möchten, wählen Sie unter **Windows Server Essentials**installieren die Option **als virtuelle Instanz installieren**aus, und klicken Sie dann auf **Konfigurieren**.

2.  Der Assistent stellt einen virtuellen Computer bereit, der in etwa fünf Minuten in Anspruch nimmt.

3.  Konfigurieren Sie anschließend Windows Server Essentials, wie zuvor im Abschnitt Bereitstellen von [Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) beschrieben.


##  <a name="install-and-configure-windows-server-essentials-by-using-windows-powershell"></a><a name="BKMK_PowerShell"></a>Installieren und Konfigurieren von Windows Server Essentials mithilfe von Windows PowerShell
 Sie können die Installation von Windows Server Essentials mithilfe von Windows PowerShell-Cmdlets automatisieren.

#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>So installieren Sie Windows Server Essentials mithilfe der Windows PowerShell

1.  Öffnen Sie die Windows PowerShell-Konsole an einer Eingabeaufforderung mit erhöhten Rechten

2.  Installieren Sie die Rolle "Windows Server Essentials-Benutzer" mit dem folgenden Befehl:

    ```
    Add-WindowsFeature ServerEssentialsRole
    ```

3.  Führen Sie `Get-Help Start-WssConfigurationService` aus.

    1.  Führen Sie den folgenden Befehl aus, um die Konfiguration für das Einrichten von Windows Server Essentials als Domänencontroller zu beginnen:

        ```
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred
        ```

    2.  Führen Sie den folgenden Befehl aus, um die Konfiguration für das Einrichten von Windows Server Essentials als ein vorhandenes Domänenmitglied zu beginnen: Sie müssen ein Mitglied der Gruppe „Unternehmensadministratoren“ und der Gruppe „Domänenadministratoren“ in Active Directory sein, um diese Aufgabe auszuführen:

        ```
        Start-WssConfigurationService  œCredential <Your Credential>

        ```

4.  Überwachen Sie den Status der Installation mithilfe der folgenden Befehle:

    -   Führen Sie `Get-WssConfigurationStatus  œShowProgress`aus, damit der Installationsstatus auf der Statusanzeige angezeigt wird.

    -   Führen Sie `Get-WssConfigurationStatus`aus, um den unmittelbaren Fortschritt ohne die Statusanzeige abzurufen.

## <a name="see-also"></a>Siehe auch

-   [Neues in Windows Server Essentials](../get-started/what-s-new.md)

-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)

-   [Einstieg in Windows Server Essentials](../get-started/get-started.md)
