---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Upgrade von ADFS in Windows Server 2016
description: ''
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 39c735e9dde0fd60c7eb9ccfe0af890bdc5a5950
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838321"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>Upgrade auf AD FS in Windows Server 2016 unter Verwendung einer WID-Datenbank

>Gilt für: Windows Server 2019, Windows Server 2016


## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Upgrade von einem Windows Server 2012 R2 oder 2016-AD FS-Farm auf Windows Server-2019 
Das folgende Dokument beschreibt, wie AD FS-Farm mit AD FS in Windows Server-2019 aktualisieren, bei Verwendung eine WID-Datenbank.  

### <a name="ad-fs-farm-behavior-levels-fbl"></a>Verhalten von AD FS-Farm Ebenen (FBL)  
In AD FS für WindowsServer 2016 bietet erstmals die Farmen mit verhaltensebene (FBL). Dies ist die Einstellung für die gesamte Farm, die bestimmt, dass die Funktionen der AD FS-Farm verwenden kann. 

Die folgende Tabelle enthält die FBL Werte von Windows Server-Version:
| Windows Server-Version  | FBL | Datenbankname für AD FS-Konfiguration |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | AdfsConfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 4  | AdfsConfigurationV4 |

> [!NOTE]  
> Aktualisieren die FBL erstellt eine neue AD FS-Konfigurationsdatenbank.  Finden Sie in der obigen Tabelle, für die Namen der Konfigurationsdatenbank für jede Windows Server AD FS-Version und FBL Wert

### <a name="new-vs-upgraded-farms"></a>Neue Visual Studio aktualisiert Farmen
Standardmäßig entspricht der FBL in einer neuen AD FS-Farm den Wert für die Windows Server-Version des ersten Knotens, Farm installiert.  

AD FS-Server eine neuere Version einer AD FS 2012 R2 oder 2016-Farm hinzugefügt werden kann, und die Farm wird mit der gleichen FBL als bzw. den vorhandenen Knoten betrieben. Wenn Sie mehrere Windows Server-Versionen, die in der gleichen Farm auf den FBL-Wert, der die niedrigste Version ausgeführt haben, wird die Farm als "vermischt" werden. Allerdings werden Sie nicht die Features der späteren Versionen nutzen, bis die FBL ausgelöst wird. Mit einer mixed-Farm:  

-   Administratoren können neue Windows Server-2019 Verbundserver zu einer vorhandenen Windows Server 2012 R2 oder 2016-Farm hinzufügen. Daher wird die Farm wird im "gemischten Modus" und arbeitet auf der gleichen Farm Verhalten Ebene wie die ursprüngliche Farm. Um konsistentes Verhalten in der Farm zu gewährleisten, können nicht Features von die neueren Versionen von Windows Server AD FS konfiguriert oder verwendet werden.  

- Bevor die FBL ausgelöst werden kann, müssen Administratoren der AD FS-Knoten Windows Server-Vorgängerversionen aus der Farm entfernen.  Im Fall von einem Windows-datenbankfarm Beachten Sie, dass Sie eine der das neue Windows Server-2019 Federation Server Tp dazu höher gestuft werden auf die Rolle des primären Knoten in der Farm.

-   Sobald alle Verbundserver in der Farm die gleiche Version von Windows Server sind, kann die FBL ausgelöst werden.  Daher können keine neuen Features von AD FS-Windows-Server 2019 dann konfiguriert und verwendet werden.

Denken Sie daran, dass im Farmmodus mit gemischten, AD FS-Farm nicht keine neuen Features oder Funktionen, eingeführt in AD FS unter Windows Server-2019 möglich ist. Dies bedeutet, dass Organisationen, die neuen Features ausprobieren möchten dies nicht möglich, bis die FBL ausgelöst wird. Wenn Ihre Organisation suchen wird, um die neuen Features vor der FBL rasing testen, müssen Sie daher eine separate Farm zu diesem Zweck bereitgestellt.  

Der Rest der ist Dokument enthält die Schritte zum Hinzufügen eines Verbundservers 2019 für Windows Server 2012 R2-Umgebung zu Windows Server 2016, und klicken Sie dann das Auslösen der FBL auf Windows Server-2019. Diese Schritte wurden in einer testumgebung beschrieben, die durch das folgende Architekturdiagramm ausgeführt.  

> [!NOTE]  
> Bevor Sie zu AD FS unter Windows Server 2019 FBL verschieben können, müssen Sie alle Windows Server 2016 oder 2012 R2-Knoten entfernen. Sie können nicht nur upgrade von Windows Server 2016 oder 2012 R2-Betriebssystem auf Windows Server-2019 und ihm eine 2019 Knoten. Sie benötigen, zu entfernen und Ersetzen Sie ihn durch einen neuen 2019-Knoten.



##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>Upgrade von AD FS-Farm auf Windows Server 2019 Farmen mit Verhaltensebene  

1.  Installieren Sie die Active Directory Federation Services-Rolle mit Server-Manager auf dem Windows Server-2019 

2.  Verknüpfen Sie den neuen Server mit Windows Server-2019 mithilfe des Assistenten für die AD FS-Konfiguration mit vorhandenen AD FS-Farm an.  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Öffnen Sie auf dem Verbundserver 2019 für Windows Server AD FS-Verwaltung. Beachten Sie, dass Funktionen nicht verfügbar sind, da dieser Verbundserver nicht auf dem primären Server ist.  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  Öffnen Sie auf dem Windows Server-2019-Server ein PowerShell-Befehlsfenster mit erhöhten Rechten, und führen Sie das folgende Cmdlet: `Set-AdfsSyncProperties -Role PrimaryComputer`

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  Klicken Sie auf der AD FS-Server, der zuvor als primär konfiguriert wurde, öffnen Sie ein PowerShell-Befehlsfenster mit erhöhten Rechten, und führen Sie das folgende Cmdlet: `Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN} `

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  Konfigurieren Sie auf jedes Webanwendungsproxys, erneut die WAP durch den folgenden PowerShell-Befehl in einem Fenster mit erhöhten Rechten ausführen:  
```powershell
$trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
```

7.  Öffnen Sie jetzt auf dem Windows Server 2016-Verbundserver AD FS-Verwaltung. Beachten Sie, dass jetzt alle Administratorfunktionen angezeigt werden, da die primäre Rolle auf diesem Server übertragen wurde.  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

8.  Wenn Sie eine AD FS-Farm mit 2012 R2 auf 2016 oder 2019 aktualisieren, erfordert das Farmupgrade das AD-Schema, sein mindestens Ebene 85.  Um das Schema, mit der Windows Server 2016-Installationsmedien zu aktualisieren, öffnen Sie eine Eingabeaufforderung, und navigieren Sie zu Support\adprep Verzeichnis. Führen Sie Folgendes:  `adprep /forestprep`

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

    Führen Sie nach Abschluss des `adprep/domainprep`
    >[!NOTE]
    >Sicherstellen Sie bevor der nächste Schritt ausgeführt wird, dass Windows Server aktuelle durch Ausführen von Windows Update aus den Einstellungen. Setzen Sie diesen Prozess fort, bis keine weiteren Updates benötigt werden. 
    > 
    
    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

9. Klicken Sie jetzt auf dem Windows Server 2016-Server öffnen Sie PowerShell, und führen Sie das folgende Cmdlet:
    >[!NOTE]
    > Alle 2012 R2-Server müssen aus der Farm entfernt werden, bevor der nächste Schritt ausgeführt wird.
 
    `Invoke-AdfsFarmBehaviorLevelRaise`  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

10. Geben Sie bei Aufforderung Y. Dadurch wird das Auslösen der Ebene gestartet. Sobald dies abgeschlossen ist, haben Sie erfolgreich die FBL ausgelöst.  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

11. Nun, wenn Sie AD FS-Verwaltung öffnen, sehen Sie, dass die neuen Funktionen für die neuere Version von AD FS hinzugefügt wurden 

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

13. Ebenso können Sie die PowerShell-Cmdlet: `Get-AdfsFarmInformation` soll Ihnen zeigen, dass die aktuelle FBL können.  

    ![Upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  
    

