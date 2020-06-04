---
title: Aktualisieren auf AD FS in Windows Server 2016 mit SQL Server
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 090e5c9ffbbaaa6720eb8e938019c08baff681cf
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333931"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>Aktualisieren auf AD FS in Windows Server 2016 mit SQL Server


> [!NOTE]  
> Starten Sie nur ein Upgrade mit einem definitiv vorgesehenen Zeitrahmen, der abgeschlossen werden soll. Es wird nicht empfohlen, die AD FS für einen längeren Zeitraum in einem Zustand mit gemischtem Modus beizubehalten, da das belassen AD FS in einem Zustand im gemischten Modus Probleme mit der Farm verursachen kann.


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Wechsel von einer Windows Server 2012 R2 AD FS-Farm zu einer Windows Server 2016 AD FS-Farm  
Im folgenden Dokument wird beschrieben, wie Sie Ihre AD FS Windows Server 2012 R2-Farm auf AD FS in Windows Server 2016 aktualisieren, wenn Sie eine SQL Server für die AD FS-Datenbank verwenden.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Aktualisieren von AD FS auf Windows Server 2016 FBL  
Neu in AD FS für Windows Server 2016 ist die Funktion für die Farm Verhaltens Stufe (SBL).   Diese Features sind Farm weit und bestimmen die Features, die von der AD FS-Farm verwendet werden können.   Standardmäßig befindet sich der SBL in einer Windows Server 2012 R2-AD FS-Farm unter Windows Server 2012 R2.  

Ein Windows Server 2016 AD FS-Server kann einer Windows Server 2012 R2-Farm hinzugefügt werden, und er wird auf derselben FBL wie Windows Server 2012 R2 ausgeführt.  Wenn Sie einen Windows Server 2016 AD FS Server auf diese Weise betreiben, wird die Farm als "gemischt" bezeichnet.  Sie können jedoch erst die neuen Windows Server 2016-Features nutzen, wenn die FBL auf Windows Server 2016 hoch geschaltet wird.  Mit einer gemischten Farm:  

-   Administratoren können einer vorhandenen Windows Server 2012 R2-Farm neue Windows Server 2016-Verbund Server hinzufügen.  Daher befindet sich die Farm im gemischten Modus und arbeitet die Verhaltensebene der Windows Server 2012 R2-Farm.  Um ein konsistentes Verhalten in der Farm sicherzustellen, können neue Windows Server 2016-Features in diesem Modus nicht konfiguriert oder verwendet werden.  

-   Nachdem alle Windows Server 2012 R2-Verbund Server aus der Farm im gemischten Modus entfernt wurden und im Fall einer wid-Farm einer der neuen Verbund Server mit Windows-Dienst 2016 auf die Rolle des primären Knotens herauf gestuft wurde, kann der Administrator den FBL von Windows Server 2012 R2 auf Windows Server 2016 herauf Stufen.  Folglich können alle neuen AD FS Windows Server 2016-Features konfiguriert und verwendet werden.  

-   Aufgrund der Funktion für gemischte Farmen AD FS Windows Server 2012 R2-Unternehmen, die ein Upgrade auf Windows Server 2016 durchführen möchten, keine vollständig neue Farm bereitstellen und Konfigurationsdaten exportieren und importieren.  Stattdessen können Sie Windows Server 2016-Knoten zu einer vorhandenen Farm hinzufügen, während Sie online ist, und nur die relativ kurze Ausfallzeit der FBL auslösen.  

Beachten Sie, dass die AD FS-Farm im gemischten Farm Modus keine neuen Features oder Funktionen bietet, die in AD FS in Windows Server 2016 eingeführt wurden.  Dies bedeutet, dass Unternehmen, die neue Features ausprobieren möchten, dies erst tun können, wenn die FBL ausgelöst wird.  Wenn Ihre Organisation also die neuen Features testen möchte, bevor Sie den FBL Rachen, müssen Sie hierfür eine separate Farm bereitstellen.  

Der Rest des Dokuments ist die Schritte zum Hinzufügen eines Windows Server 2016-Verbund Servers zu einer Windows Server 2012 R2-Umgebung und zum anschließenden erhöhen des FBL an Windows Server 2016.  Diese Schritte wurden in einer Testumgebung ausgeführt, die im folgenden Architektur Diagramm beschrieben wird.  

> [!NOTE]  
> Bevor Sie zu AD FS in Windows Server 2016 FBL wechseln können, müssen Sie alle Windows 2012 R2-Knoten entfernen.  Es ist nicht möglich, ein Windows Server 2012 R2-Betriebssystem auf Windows Server 2016 zu aktualisieren und es zu einem 2016-Knoten zu werden.  Sie müssen ihn entfernen und durch einen neuen 2016-Knoten ersetzen.  

Das folgende Architektur Diagramm zeigt das Setup, das zum Überprüfen und Aufzeichnen der nachfolgenden Schritte verwendet wurde.

![Aufbau](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png)


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Fügen Sie den Windows 2016 AD FS Server der AD FS Farm hinzu.

1.  Installieren Sie mithilfe Server-Manager die Active Directory-Verbunddienste (AD FS) Rolle auf Windows Server 2016.  

2.  Fügen Sie mit dem Konfigurations-Assistenten für AD FS den neuen Windows Server 2016-Server der vorhandenen AD FS Farm hinzu.  Klicken Sie auf der **Willkommens** Seite auf **weiter**.
 ![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  Auf dem Bildschirm **mit Active Directory Domain Services verbinden** wird**ein Administrator Konto** mit Berechtigungen zum Durchführen der Verbund Dienst Konfiguration angezeigt, und klicken Sie auf **weiter**.
4.  Geben Sie auf dem Bildschirm **Farm angeben** den Namen des SQL-Servers und der Instanz ein, und klicken Sie dann auf **weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  Geben Sie auf dem Bildschirm **SSL-Zertifikat angeben** das Zertifikat an, und klicken Sie auf **weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  Geben Sie auf dem Bildschirm **Dienst Konto angeben** das Dienst Konto an, und klicken Sie auf **weiter**.
7.  Überprüfen Sie auf dem Bildschirm **Überprüfungs Optionen** die Optionen, und klicken Sie auf **weiter**.
8.  Vergewissern Sie sich, dass auf dem Bildschirm **Voraussetzungs Prüfungen** alle erforderlichen Überprüfungen erfolgreich waren, und klicken Sie dann auf **Konfigurieren**.
9.  Stellen Sie auf dem Bildschirm **Ergebnisse** sicher, dass der Server erfolgreich konfiguriert wurde, und klicken Sie auf **Schließen**.


#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS Server entfernen

>[!NOTE]
>Sie müssen den primären AD FS Server nicht mithilfe von "Set-adfssyncproperties-Role" festlegen, wenn Sie SQL als Datenbank verwenden.  Dies liegt daran, dass alle Knoten in dieser Konfiguration als primär eingestuft werden.

1.  Verwenden Sie auf dem Windows Server 2012 R2-AD FS Server in Server-Manager die Option **Rollen und Features** unter **Verwalten**.
![Server entfernen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  Klicken Sie auf dem Bildschirm **Vorbemerkungen** auf **Weiter**.
3.  Klicken Sie auf dem Bildschirm **Server Auswahl** auf **weiter**.
4.  Entfernen Sie auf dem Bildschirm **Server Rollen** die Option neben **Active Directory-Verbunddienste (AD FS)** , und klicken Sie auf **weiter**.
![Server entfernen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  Klicken Sie auf dem Bildschirm **Features** auf **weiter**.
6.  Klicken Sie auf dem **Bestätigungs** Bildschirm auf **Entfernen**.
7.  Nachdem dieser Vorgang abgeschlossen ist, starten Sie den Server neu.

#### <a name="raise-the-farm-behavior-level-fbl"></a>Erhöhen der Farm Verhaltensebene (SBL)
Vor diesem Schritt müssen Sie sicherstellen, dass ForestPrep und DomainPrep in Ihrer Active Directory Umgebung ausgeführt wurden und dass Active Directory über das Schema Windows Server 2016 verfügt.  Dieses Dokument wurde mit einem Windows 2016-Domänen Controller gestartet und erforderte diese Ausführung nicht, da Sie bei der Installation von AD ausgeführt wurden.

>[!NOTE]
>Vergewissern Sie sich vor dem Starten des nachfolgenden Prozesses, dass Windows Server 2016 aktuell ist, indem Sie Windows Update von Einstellungen ausführen.  Setzen Sie diesen Prozess fort, bis keine weiteren Updates erforderlich sind. Stellen Sie außerdem sicher, dass das Konto des AD FS-Dienst Kontos über die Administrator Berechtigungen für den SQL-Server und jeden Server in der AD FS-Farm verfügt.

1. Öffnen Sie nun auf dem Windows Server 2016-Server PowerShell, und führen Sie den folgenden Befehl aus: **$cred = Get-Credential** und drücken Sie die EINGABETASTE.
2. Geben Sie Anmelde Informationen ein, die auf dem SQL Server über Administratorrechte verfügen.
3. Geben Sie nun in PowerShell Folgendes ein: **aufrufen-adfsfarmverhalorlevelraise-Credential $cred**
2. Geben Sie bei entsprechender Aufforderung **Y**ein.  Dadurch wird die Ebene erhöht.  Nachdem dieser Vorgang abgeschlossen ist, haben Sie die voll qualifizierte vollständig ausgelöst.  
![Update abschließen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. Wenn Sie nun AD FS Verwaltung wechseln, werden die neuen Knoten angezeigt, die für AD FS in Windows Server 2016 hinzugefügt wurden.  
4. Ebenso können Sie das PowerShell-Cmdlet "Get-adfsfarminformation" verwenden, um den aktuellen FBL anzuzeigen.  
![Update abschließen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)

#### <a name="upgrade-the-configuration-version-of-existing-wap-servers"></a>Aktualisieren der Konfigurations Version vorhandener WAP-Server
1. Konfigurieren Sie auf jedem webanwendungsproxy den WAP neu, indem Sie den folgenden PowerShell-Befehl in einem erhöhten Fenster ausführen:  
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
    ```
2. Entfernen Sie alte Server aus dem Cluster, und behalten Sie nur die WAP-Server, auf denen die neueste Server Version ausgeführt wird, die oben neu konfiguriert wurde, durch Ausführen des folgenden PowerShell-Cmdlets.
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
3. Überprüfen Sie die WAP-Konfiguration, indem Sie das Cmdlet Get-webapplicationproxyconfiguration ausführen. Connectedserversname gibt den Server an, der mit dem vorherigen Befehl ausgeführt wurde.
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
4. Führen Sie den folgenden PowerShell-Befehl aus, um die configurationversion der WAP-Server zu aktualisieren.
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
5. Vergewissern Sie sich, dass configurationversion mit dem PowerShell-Befehl Get-webapplicationproxyconfiguration aktualisiert wurde.
