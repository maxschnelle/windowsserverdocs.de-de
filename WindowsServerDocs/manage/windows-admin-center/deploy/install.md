---
title: Installieren von Windows Admin Center
description: So installieren Sie Windows Admin Center auf einem Windows-PC oder Server.
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 496a67cfb93bf9b42b202f6a61211a085a9253b6
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296692"
---
# Installieren von Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## Ordnen Sie Ihre installation

Überprüfen Sie die [Optionen für die Installation](..\plan\installation-options.md) die enthält die [unterstützten Betriebssystemen](..\plan\installation-options.md#supported-operating-systems-installation). Zum Installieren von Windows Admin Center auf einem virtuellen Computer in Azure finden Sie unter " [Bereitstellen von Windows Admin Center in Azure](../azure/deploy-wac-in-azure.md)".

## Installieren unter Windows 10

Bei der Installation von Windows Admin Center auf Windows 10 wird standardmäßig Port 6516 verwendet, aber Sie haben die Möglichkeit, einen anderen Port anzugeben. Sie können auch eine Desktopverknüpfung erstellen und lassen Windows Admin Center Ihren TrustedHost verwalten.

> [!NOTE]
> Für das Ändern des TrustedHosts ist eine Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Wenn Sie Windows Admin Center über **das Startmenü** starten, wird es in Ihrem Standardbrowser geöffnet.

Wenn Sie Windows Admin Center zum ersten Mal starten, sehen Sie ein Symbol im Benachrichtigungsbereich Ihres Desktops. Klicken Sie mit der rechten Maustaste auf dieses Symbol, und wählen Sie **Öffnen**, um das Tool in Ihrem Standardbrowser zu öffnen, oder wählen Sie **Beenden**, um den Hintergrundprozess zu beenden.

## Installieren Sie auf Windows Server mit Desktopdarstellung

Unter Windows Server wird Windows Admin Center als Netzwerkdienst installiert. Geben Sie den Port an, den der Dienst überwacht und dies erfordert ein Zertifikat für HTTPS. Das Installationsprogramm kann zu Testzwecken ein selbstsigniertes Zertifikat erstellen, oder Sie können den Fingerabdruck eines Zertifikats bereitstellen, der bereits auf dem Computer installiert ist. Wenn Sie das generierte Zertifikat verwenden, wird es den DNS-Namen des Servers entsprechen. Wenn Sie Ihr eigenes Zertifikat verwenden, stellen Sie sicher, dass der bereitgestellten Namen im Zertifikat entspricht, den Computernamen (Platzhalterzeichen Zertifikate werden nicht unterstützt.) Sie haben die Möglichkeit, Windows Admin Center Ihre TrustedHosts verwalten lassen.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Sobald die Installation abgeschlossen ist, öffnen Sie einen Browser von einem Remotecomputer, und navigieren Sie zu URL, die im letzten Schritt des Installers angezeigt.

> [!WARNING]
> Automatisch generierte Zertifikate werden 60 Tage nach der Installation ungültig.

## Installieren Sie auf Server Core

Wenn Sie über die Server Core-Installationsoption von Windows Server verfügen, können Sie Windows Admin Center über die Befehlszeile (als Administrator ausführen) installieren. Legen Sie einen Port und SSL-Zertifikat mithilfe der `SME_PORT` und `SSL_CERTIFICATE_OPTION`-Argumente fest. Wenn Sie ein vorhandenes Zertifikat verwenden, verwenden Sie `SME_THUMBPRINT`, um einen Fingerabdruck anzugeben.

> [!WARNING]
> Installieren von Windows Admin Center wird den WinRM-Dienst neu starten, der wodurch alle PowerShells Remotesitzungen Server wird. Es wird empfohlen, dass Sie von einem lokalen Cmd oder PowerShell installieren. Wenn Sie mit einer Lösung für die Benutzeroberflächenautomatisierung installieren, die durch das erneute Starten WinRM-Dienst umbrochen werden würde, können Sie den Parameter hinzufügen ```RESTART_WINRM=0``` für die Installation Argumente, aber WinRM muss neu gestartet werden für Windows Admin Center Funktion.

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center aus und um automatisch ein selbstsigniertes Zertifikat zu generieren:

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center mit einem vorhandenen Zertifikat aus:

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> Das Aufrufen von `msiexec` über PowerShell mit Punkt-Schrägstrich-Notation für relative Pfade (z.B. `.\<WindowsAdminCenterInstallerName>.msi`) ist nicht möglich. Diese Notation wird nicht unterstützt, und die Installation schlägt fehl. Entfernen Sie das Präfix `.\` oder geben Sie den vollständigen Pfad zur MSI-Datei an.

## Aktualisieren von Windows Admin Center

Sie können nicht-Vorschauversion von Windows Admin Center aktualisieren, mithilfe von Microsoft Update oder manuell installieren. 

Ihre Einstellungen bleiben, beim Upgrade auf eine neue Version von Windows Admin Center. Wir nicht offiziell unterstützt das Aktualisieren Insider Preview-Versionen von Windows Admin Center – wir glauben, dass es besser, eine Neuinstallation - durchgeführt wird, aber wir nicht blockieren.