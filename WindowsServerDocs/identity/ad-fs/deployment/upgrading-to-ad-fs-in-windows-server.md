---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Upgrade von ADFS in Windows Server 2016
description: ''
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 428e35524fbcfe5177b544e1c6cc6fa32ec32056
ms.sourcegitcommit: 4a03f263952c993dfdf339dd3491c73719854aba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2019
ms.locfileid: "74791368"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>Upgrade auf AD FS in Windows Server 2016 unter Verwendung einer WID-Datenbank


> [!NOTE]
> Starten Sie nur ein Upgrade mit einem definitiv vorgesehenen Zeitrahmen, der abgeschlossen werden soll. Es wird nicht empfohlen, die AD FS für einen längeren Zeitraum in einem Zustand mit gemischtem Modus beizubehalten, da das belassen AD FS in einem Zustand im gemischten Modus Probleme mit der Farm verursachen kann.

## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Aktualisieren einer Windows Server 2012 R2-oder 2016 AD FS-Farm auf Windows Server 2019
Im folgenden Dokument wird beschrieben, wie Sie Ihre AD FS-Farm auf AD FS in Windows Server 2019 aktualisieren, wenn Sie eine wid-Datenbank verwenden.

### <a name="ad-fs-farm-behavior-levels-fbl"></a>AD FS-Farm Verhaltens Stufen (SBL)
In AD FS für Windows Server 2016 wurde die Farm Verhaltensebene (SBL) eingeführt. Dies ist eine Farm weite Einstellung, mit der die Funktionen bestimmt werden, die die AD FS-Farm verwenden kann.

In der folgenden Tabelle sind die FBL-Werte nach Windows Server-Version aufgeführt:

| Windows Server-Version  | Mit der Bezeichnung | Name der AD FS Konfigurations Datenbank |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | Adfsconfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 4  | AdfsConfigurationV4 |

> [!NOTE]
> Bei einem Upgrade des-Daten Bank Upgrades wird eine neue AD FS Konfigurations Datenbank erstellt.  In der obigen Tabelle finden Sie die Namen der Konfigurations Datenbank für die einzelnen Windows Server-AD FS Version und den FBL-Wert.

### <a name="new-vs-upgraded-farms"></a>Neue im Vergleich zu aktualisierten Farmen
Standardmäßig stimmt der voll qualifizierte Namen in einer neuen AD FS Farm mit dem Wert für die Windows Server-Version des ersten installierten Farm Knotens überein.

Ein AD FS Server einer höheren Version kann mit einer AD FS 2012 R2-oder 2016-Farm verknüpft werden, und die Farm wird in derselben FBL wie die vorhandenen Knoten ausgeführt. Wenn Sie mehrere Windows Server-Versionen in derselben Farm mit dem FBL-Wert der niedrigsten Version betreiben, wird die Farm als "gemischt" bezeichnet. Sie sind jedoch nicht in der Lage, die Features der späteren Versionen zu nutzen, bis die FBL ausgelöst wird. Mit einer gemischten Farm:

- Administratoren können einer vorhandenen Windows Server 2012 R2-oder 2016-Farm neue Windows Server 2019-Verbund Server hinzufügen. Daher befindet sich die Farm im gemischten Modus und funktioniert auf derselben Farm Verhaltensebene wie die ursprüngliche Farm. Um ein konsistentes Verhalten in der Farm sicherzustellen, können die Features der neueren Windows Server-AD FS Versionen nicht konfiguriert oder verwendet werden.

- Vor dem Löschen der-Datei müssen Administratoren die AD FS Knoten vorheriger Windows Server-Versionen aus der Farm entfernen.  Beachten Sie bei einer wid-Farm, dass eine der neuen Windows Server 2019-Verbund Server in die Rolle des primären Knotens in der Farm herauf gestuft werden muss.

- Wenn alle Verbund Server in der Farm die gleiche Windows Server-Version aufweisen, kann der voll qualifizierte Schlüssel Name ausgelöst werden.  Folglich können alle neuen AD FS Windows Server 2019-Features konfiguriert und verwendet werden.

Beachten Sie, dass die AD FS-Farm im gemischten Farm Modus keine neuen Features oder Funktionen bietet, die in AD FS in Windows Server 2019 eingeführt wurden. Dies bedeutet, dass Unternehmen, die neue Features ausprobieren möchten, dies erst tun können, wenn die FBL ausgelöst wird. Wenn Ihre Organisation also die neuen Features testen möchte, bevor Sie die FBL erhöhen, müssen Sie hierfür eine separate Farm bereitstellen.

Der Rest des Dokuments enthält die Schritte zum Hinzufügen eines Windows Server 2019-Verbund Servers zu einer Windows Server 2016-oder 2012 R2-Umgebung und zum anschließenden erhöhen des FBL auf Windows Server 2019. Diese Schritte wurden in einer Testumgebung ausgeführt, die im folgenden Architektur Diagramm beschrieben wird.

> [!NOTE]
> Bevor Sie zu AD FS in Windows Server 2019 FBL wechseln können, müssen Sie alle Windows Server 2016-oder 2012 R2-Knoten entfernen. Sie können ein Windows Server 2016-oder 2012 R2-Betriebssystem nicht einfach auf Windows Server 2019 aktualisieren und als Knoten "2019" festlegen. Sie müssen ihn entfernen und durch einen neuen 2019-Knoten ersetzen.

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>So führen Sie ein Upgrade Ihrer AD FS Farm auf die Windows Server 2019-Farm Verhaltensebene aus

1. Installieren Sie mithilfe Server-Manager die Active Directory-Verbunddienste (AD FS) Rolle auf Windows Server 2019.

2. Fügen Sie mit dem Konfigurations-Assistenten für AD FS den neuen Windows Server 2019-Server der vorhandenen AD FS Farm hinzu.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)

3. Öffnen Sie auf dem Windows Server 2019-Verbund Server AD FS-Verwaltung. Beachten Sie, dass Verwaltungsfunktionen nicht verfügbar sind, da es sich bei diesem Verbund Server nicht um den primären Server handelt.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)

4. Öffnen Sie auf dem Windows Server 2019-Server ein PowerShell-Befehlsfenster mit erhöhten Rechten, und führen Sie das folgende Cmdlet aus:

```PowerShell
Set-AdfsSyncProperties -Role PrimaryComputer
```

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)

5. Öffnen Sie auf dem AD FS Server, der zuvor als primär konfiguriert wurde, ein PowerShell-Befehlsfenster mit erhöhten Rechten, und führen Sie das folgende Cmdlet aus:

```PowerShell
Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN}
```

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)

6. Öffnen Sie nun auf dem Windows Server 2016-Verbund Server AD FS-Verwaltung. Beachten Sie, dass jetzt alle Administrator Funktionen angezeigt werden, da die primäre Rolle auf diesen Server übertragen wurde.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)

7. Wenn Sie eine AD FS 2012 R2-Farm auf 2016 oder 2019 aktualisieren, erfordert das Farm Upgrade, dass das AD-Schema mindestens die Ebene 85 hat.  Öffnen Sie zum Aktualisieren des Schemas mit dem Windows Server 2016-Installationsmedium eine Eingabeaufforderung, und navigieren Sie zum Verzeichnis support\adprep. Führen Sie Folgendes aus: `adprep /forestprep`

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)

Wenn die Ausführung abgeschlossen ist, `adprep/domainprep`

> [!NOTE]
> Stellen Sie vor dem Ausführen des nächsten Schritts sicher, dass Windows Server aktuell ist, indem Sie Windows Update aus den Einstellungen ausführen. Setzen Sie diesen Prozess fort, bis keine weiteren Updates benötigt werden.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)

8. Öffnen Sie nun auf dem Windows Server 2016-Server PowerShell, und führen Sie das folgende Cmdlet aus:

> [!NOTE]
> Alle 2012 R2-Server müssen vor dem Ausführen des nächsten Schritts aus der Farm entfernt werden.

```PowerShell
Invoke-AdfsFarmBehaviorLevelRaise
```

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)

9. Geben Sie bei entsprechender Aufforderung Y ein. Dadurch wird die Ebene erhöht. Nachdem dieser Vorgang abgeschlossen ist, haben Sie die voll qualifizierte vollständig ausgelöst.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)

10. Wenn Sie nun AD FS Verwaltung wechseln, sehen Sie, dass die neuen Funktionen für die spätere AD FS Version hinzugefügt wurden.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)

11. Ebenso können Sie das PowerShell-Cmdlet verwenden: `Get-AdfsFarmInformation`, um Ihnen den aktuellen FBL anzuzeigen.

![upgraden](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)

12. Um die WAP-Server auf die neueste Ebene zu aktualisieren, konfigurieren Sie auf jedem webanwendungsproxy den WAP neu, indem Sie das folgende PowerShell-Cmdlet in einem erweiterten Fenster ausführen:

```PowerShell
$trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred
```

Entfernen Sie alte Server aus dem Cluster, und behalten Sie nur die WAP-Server bei, auf denen die neueste Server Version ausgeführt wird, die oben neu konfiguriert wurde, indem Sie das folgende PowerShell-Cmdlet ausführen.

```PowerShell
Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
```

Überprüfen Sie die WAP-Konfiguration, indem Sie das Cmdlet Get-webapplicationproxyconfiguration ausführen. Connectedserversname gibt den Server an, der mit dem vorherigen Befehl ausgeführt wurde.

```PowerShell
Get-WebApplicationProxyConfiguration
```
Führen Sie den folgenden PowerShell-Befehl aus, um die configurationversion der WAP-Server zu aktualisieren.

```PowerShell
Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
```

Dadurch wird das Upgrade der WAP-Server beendet.
