---
title: Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8a2310b178663c6ca32a4e07d11656f1aaf2a11b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844411"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials ist ein idealer erster Server für kleine Unternehmen mit bis zu 25 Benutzern und 50 Geräten. Für Organisationen mit bis zu 100 Benutzern und 200 Geräten können Sie jetzt Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle. Dieses Thema zielt auf beide Szenarien ab.  
  
Windows Server Essentials Experience ist eine Rolle in Windows Server 2016, mit dem Sie alle Features (wie Remotewebzugriff und PC-Sicherung) nutzen, die finden Sie in Windows Server Essentials ohne Sperren und Beschränkungen, die in erzwungen werden  Windows Server Essentials. Diese Serverrolle steht auch in Windows Server Essentials und ist standardmäßig aktiviert.
  
Bevor Sie Windows Server Essentials oder die Essentials Experience-Rolle installieren, beachten Sie die folgenden Einschränkungen.  
  
|Windows Server Essentials-Umgebung in Windows Server Essentials|Windows Server Essentials Experience unter WindowsServer 2016
|----|----|
|-Muss der Domänencontroller am Stamm der Gesamtstruktur und Domäne sein und muss alle FSMO-Rollen.<br /><br /> -Kann nicht in einer Umgebung mit einer vorhandenen Active Directory-Domäne installiert werden (es ist jedoch eine Karenzzeit von 21 Tagen zum Durchführen von Migrationen).|-Muss kein Domänencontroller fungieren, wenn es in einer Umgebung mit einer vorhandenen Active Directory-Domäne installiert ist.<br /><br /> – Wenn es sich um eine Active Directory-Domäne nicht vorhanden ist, wird bei Installation der Rolle Active Directory-Domäne erstellt, und der Server wird der Domänencontroller am Stamm der Gesamtstruktur und Domäne, enthält alle FSMO-Rollen.  
|Kann nur in einer einzelnen Domäne bereitgestellt werden.|Kann nur in einer einzelnen Domäne bereitgestellt werden.  
|In Ihrer Domäne darf kein schreibgeschützter Domänencontroller vorhanden sein.|In Ihrer Domäne darf kein schreibgeschützter Domänencontroller vorhanden sein.

> [!NOTE]
>  Besuchen Sie zum Herunterladen von Evaluierungsversionen des Betriebssystems das TechNet Evaluierungscenter :  
>   
>  [Laden Sie WindowsServer 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials herunterladen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>Installationsoptions  
 Dieses Dokument enthält schrittweise Anleitungen zum Installieren und Konfigurieren von Windows Server Essentials. In Abhängigkeit Ihrer Netzwerkumgebung stehen Ihnen die folgenden Installationsoptionen zur Verfügung:  
  
-    Windows Server Essentials (mit der Windows Server Essentials Experience-Rolle in der Standardeinstellung aktiviert)  
  
-    Windows Server 2016 mit installierter Windows Server Essentials Experience-Rolle  
 
|Bereitstellungsumgebung|Beschreibung|Zugehöriger Abschnitt|  
|----------------------------|-----------------|---------------------|  
|Neue Active Directory-Umgebung|Sie können Windows Server Essentials zum Erstellen einer neuen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|Vorhandene Active Directory-Umgebung|Sie können Windows Server Essentials in einer vorhandenen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|Virtuelle Umgebung|Sie können Windows Server Essentials als virtuellen Computer bereitstellen.|[Ihre Umgebung zu virtualisieren](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|Automatisierte Bereitstellung|Sie können die Bereitstellung von Windows Server Essentials mithilfe der Windows PowerShell automatisieren.|[Installieren und Konfigurieren von Windows Server Essentials mithilfe von Windows PowerShell](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>Vorbemerkungen  
 Lesen Sie vor dem Installieren die folgende Dokumentation:  
  
-   [Windows Server Essentials – Produktübersicht](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Systemanforderungen für Windows Server Essentials](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a> Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory-Umgebung  
 Windows Server Essentials bietet Ihnen die Möglichkeit, eine Active Directory-Umgebung und zugehörige Serverfeatures schnell einzurichten.  
  
###  <a name="BKMK_WSEDeploy"></a> Bereitstellen von Windows Server Essentials  
 Wenn Sie Windows Server Essentials verwenden, ist Windows Server Essentials Experience bereits aktiviert. Sie müssen jedoch einige Schritte abschließen, um Ihren Server zu konfigurieren.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>So konfigurieren Sie Windows Server Essentials auf einem physischen server  
  
1.  Im Anschluss an die Windows-Startseite**** wird der Assistent für die Konfiguration von Windows Server Essentials**** auf Ihrem Desktop angezeigt.  
  
2.  Befolgen Sie die Anweisungen, um den Assistenten wie folgt abzuschließen:  
  
    1.  Klicken Sie auf der Seite **Windows Server Essentials konfigurieren** auf **Weiter**.  
  
    2.  Stellen Sie unter **Uhrzeiteinstellungen**sicher, dass Datum, Uhrzeit und Zeitzone richtig sind, und klicken Sie dann auf **Weiter**.  
  
    3.  Geben Sie unter **Firmeninformationen**Ihren Unternehmensnamen wie **Contoso,Ltd.** ein, und klicken Sie dann auf **Weiter**. Optional können Sie den internen Domänennamen und den Servernamen ändern.  
  
    4.  Geben Sie unter der Option zum Erstellen eines Netzwerkadministrators **** einen neuen Administratorkontonamen und ein -kennwort ein.  
  
        > [!NOTE]
        >  Verwenden Sie nicht den bzw. das standardmäßige(n) **Administrator**-Kontonamen und -kennwort.  
  
    5.  Klicken Sie auf **Konfigurieren**.  
  
3.  Während des Konfigurationsvorgangs wird der Server mehrfach neu gestartet, und Ihre Anmeldungen erfolgen automatisch, bis die Konfiguration abgeschlossen ist. Dieser Vorgang nimmt etwa 20 Minuten in Anspruch.  
  
4.  Klicken Sie auf dem Desktop auf das Dashboardsymbol, um das Serverdashboard zu starten. Schließen Sie auf der Startseite**** die Aufgaben **Erste Schritte** ab, die auf der Registerkarte **Einrichtung** aufgelistet sind.  
  
 Nach Abschluss der Serverkonfiguration wird der Server, auf dem Windows Server Essentials ausgeführt wird, als Domänencontroller festgelegt.  
  
###  <a name="BKMK_DeployWSERole"></a> Bereitstellen der Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard und Datacenter  
 Sie können die Server-Manager verwenden, aktivieren und Konfigurieren von Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mithilfe des folgenden Verfahrens.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>So stellen Sie die Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 bereit  
  
1.  Melden Sie sich an Ihrem Server als ein lokaler Administrator an.  
  
2.  Öffnen Sie **Server-Manager**, und klicken Sie dann auf **Rollen und Features hinzufügen**.  
  
3.  Wählen Sie in **Serverrollen auswählen**die Rolle **Windows Server Essentials Experience** aus. Klicken Sie im Dialogfeld auf **Features hinzufügen**und dann auf **Weiter**.  
  
4.  Klicken Sie in **Features**auf **Weiter**.  
  
5.  Prüfen Sie die Rollenbeschreibung **Windows Server Essentials Experience** , und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf den Seiten, die darauf folgen, auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **Installieren**.  
  
7.  Nachdem die Installation abgeschlossen ist, sollte Windows Server Essentials Experience als Serverrolle im Server-Manager aufgeführt werden.  
  
8.  Klicken Sie im Bereich für die Kennzeichnungsbenachrichtigung im Server-Manager auf die Kennzeichnung, und klicken Sie dann auf **Windows Server Essentials konfigurieren**.  
  
9. (Optional) Ändern Sie bei Bedarf den Servernamen.  
  
    > [!IMPORTANT]
    >  Sie können den Servernamen nicht ändern, nachdem Sie Windows Server Essentials konfiguriert haben.  
  

10. Führen Sie den Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

10. Führen Sie den Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

  
##  <a name="BKMK_ExistingAD"></a> Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung  
 Sie können Windows Server Essentials auch bereitstellen, wenn Ihre Organisation bereits über eine vorhandene Active Directory-Umgebung verfügt. Zusätzlich können Sie sich entscheiden, ob Sie Windows Server Essentials als einen Domänencontroller bereitstellen möchten.  
  
> [!IMPORTANT]
>  Diese Option ist nur verfügbar, wenn Sie die Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter bereitstellen.  
  
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
  
6.  Wählen Sie in **Serverrollen auswählen**die Rolle **Windows Server Essentials Experience**aus. Klicken Sie im Dialogfeld auf **Features hinzufügen**und dann auf **Weiter**.  
  
7.  Klicken Sie in **Features**auf **Weiter**.  
  
8.  Prüfen Sie die Beschreibung **Windows Server Essentials Experience**, und klicken Sie dann auf **Weiter**.  
  
9. Klicken Sie auf den Seiten, die darauf folgen, auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **Installieren**.  
  
10. Nachdem die Installation abgeschlossen ist, wird Windows Server Essentials Experience als Serverrolle im Server-Manager aufgeführt.  
  
11. Klicken Sie im Meldungsinfobereich im **Server-Manager** auf Flag, und dann auf **Windows Server Essentials konfigurieren**.  
  
12. Folgen Sie dem Assistenten zum Konfigurieren von Windows Server Essentials. In Abhängigkeit Ihrer Active Directory-Konfiguration werden Sie informiert, ob Sie Windows Server Essentials auf einem Domänencontroller oder als ein Domänenmitglied konfigurieren. Klicken Sie auf **Konfigurieren**, um die Konfiguration zu beginnen. Die Konfiguration dauert ungefähr 10 Minuten.  
  
##  <a name="BKMK_VirtualWSE"></a> Ihre Umgebung zu virtualisieren  
  Windows Server Essentials, Windows Server 2012 R2 Standard und Windows Server 2012 R2 Datacenter können als virtuelle Computer ausgeführt werden. Sie können virtuelle Computer ausführen, indem Sie die Hyper-V-Verwaltungstools auf einem Server unter Hyper-V verwenden. Aus lizenzierungsperspektive ermöglicht Windows Server Essentials die Hyper-V-Rolle einzurichten und Ihre Umgebung zu virtualisieren. Die Lizenz ermöglicht Ihnen das Einrichten von einem anderen Gast-Betriebssystem, auf denen Windows Server Essentials ausgeführt wird. Je nach Ihres systemanbieters "s-Konfiguration des Windows Server Essentials können Sie nahtlose Einrichtung einer virtualisierten Umgebung.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>So stellen Sie Windows Server Essentials als einen virtuellen Computer bereit  
  
1.  Nach der Windows-Startseite (je nach "Konfiguration des Systems Provider des s) kann die **vor dem Beginn** Seite enthält eine Option zum Einrichten von Windows Server Essentials als eine virtuelle Instanz oder auf physischer Hardware. Die Verfügbarkeit dieser Optionen wird durch Ihren Systemanbieter vorab definiert, und beide Optionen sind möglicherweise nicht immer verfügbar. Zum Installieren von Windows Server Essentials als einen virtuellen Computer in **Installieren von Windows Server Essentials**Option **als virtuelle Instanz installieren**, und klicken Sie dann auf **konfigurieren**.  
  
2.  Der Assistent stellt einen virtuellen Computer bereit, der in etwa fünf Minuten in Anspruch nimmt.  
  

3.  Konfigurieren Sie anschließend Windows Server Essentials auf, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

3.  Konfigurieren Sie anschließend Windows Server Essentials auf, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

  
##  <a name="BKMK_PowerShell"></a> Installieren und Konfigurieren von Windows Server Essentials mithilfe von Windows PowerShell  
 Sie können die Installation von Windows Server Essentials mithilfe von Windows PowerShell-Cmdlets automatisieren.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>So installieren Sie Windows Server Essentials mithilfe der Windows PowerShell  
  
1.  Öffnen Sie die Windows PowerShell-Konsole an einer Eingabeaufforderung mit erhöhten Rechten  
  
2.  Installieren Sie Windows Server Essentials Experience-Rolle mithilfe des folgenden Befehls:  
  
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
  
    -   Führen Sie `Get-WssConfigurationStatus  œShowProgress` aus, damit der Installationsstatus auf der Statusanzeige angezeigt wird.  
  
    -   Führen Sie `Get-WssConfigurationStatus` aus, um den unmittelbaren Fortschritt ohne die Statusanzeige abzurufen.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Neuerungen in Windows Server Essentials](../get-started/what-s-new.md)  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)  
  
-   [Erste Schritte mit Windows Server Essentials](../get-started/get-started.md)
