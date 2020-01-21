---
title: Installieren von Windows Admin Center
description: Hier erfahren Sie, wie Sie Windows Admin Center auf einem Windows-PC oder auf einem Servern installieren, sodass mehrere Benutzer mit einem Webbrowser auf Windows Admin Center zugreifen können.
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: cab128a3da9fa58c598cebcdf188058631c33977
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950001"
---
# <a name="install-windows-admin-center"></a>Installieren von Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Thema wird beschrieben, wie Sie Windows Admin Center auf einem Windows-PC oder auf einem Servern installieren, sodass mehrere Benutzer mit einem Webbrowser auf Windows Admin Center zugreifen können.

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../overview.md), oder [laden Sie es jetzt herunter](https://aka.ms/windowsadmincenter).

## <a name="determine-your-installation-type"></a>Bestimmen des Installationstyps

Überprüfen Sie die [Installationsoptionen](../plan/installation-options.md), einschließlich der [unterstützten Betriebssysteme](https://docs.microsoft.com/windows-server/manage/windows-admin-center/plan/installation-options#installation-supported-operating-systems). Informationen zum Installieren von Windows Admin Center auf einem virtuellen Computer in Azure finden Sie unter [Bereitstellen von Windows Admin Center in Azure](../azure/deploy-wac-in-azure.md).

## <a name="install-on-windows-10"></a>Installieren unter Windows 10

Bei der Installation von Windows Admin Center auf Windows 10 wird standardmäßig Port 6516 verwendet, aber Sie haben die Möglichkeit, einen anderen Port anzugeben. Sie können auch eine Desktopverknüpfung erstellen und lassen Windows Admin Center Ihren TrustedHost verwalten.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Wenn Sie Windows Admin Center über **das Startmenü** starten, wird es in Ihrem Standardbrowser geöffnet.

Wenn Sie Windows Admin Center zum ersten Mal starten, wird ein Symbol im Benachrichtigungsbereich Ihres Desktops angezeigt. Klicken Sie mit der rechten Maustaste auf dieses Symbol, und wählen Sie **Öffnen**, um das Tool in Ihrem Standardbrowser zu öffnen, oder wählen Sie **Beenden**, um den Hintergrundprozess zu beenden.

## <a name="install-on-windows-server-with-desktop-experience"></a>Installieren auf Windows Server mit Desktopdarstellung

Unter Windows Server wird Windows Admin Center als Netzwerkdienst installiert. Geben Sie den Port an, den der Dienst überwacht und dies erfordert ein Zertifikat für HTTPS. Das Installationsprogramm kann zu Testzwecken ein selbstsigniertes Zertifikat erstellen, oder Sie können den Fingerabdruck eines Zertifikats bereitstellen, der bereits auf dem Computer installiert ist. Wenn Sie das generierte Zertifikat verwenden, wird es den DNS-Namen des Servers entsprechen. Wenn Sie Ihr eigenes Zertifikat verwenden, stellen Sie sicher, dass der im Zertifikat angegebene Name mit dem Computernamen übereinstimmt (Platzhalterzertifikate werden nicht unterstützt). Sie haben die Option, Ihre TrustedHosts von Windows Admin Center verwalten zu lassen.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Öffnen Sie nach Abschluss der Installation einen Browser von einem Remotecomputer aus, und navigieren Sie zur URL, die im letzten Schritt des Installers angezeigt wurde.

> [!WARNING]
> Automatisch generierte Zertifikate werden 60 Tage nach der Installation ungültig.

## <a name="install-on-server-core"></a>Installieren auf Server Core

Wenn Sie über eine Server Core-Installationsoption von Windows Server verfügen, können Sie Windows Admin Center über die Befehlszeile („Als Administrator ausführen“) installieren. Legen Sie einen Port und ein SSL-Zertifikat mithilfe der Argumente `SME_PORT` und `SSL_CERTIFICATE_OPTION` fest. Wenn Sie ein vorhandenes Zertifikat verwenden, geben Sie dessen Fingerabdruck mit `SME_THUMBPRINT` an.

> [!WARNING]
> Beim Installieren von Windows Admin Center wird der WinRM-Dienst neu gestartet, wodurch alle PowerShell-Remotesitzungen getrennt werden. Es wird empfohlen, die Installation über eine lokale Cmd oder PowerShell durchzuführen. Wenn Sie die Installation mit einer Automatisierungslösung durchführen, die den Neustart des WinRM-Diensts unterbrochen würde, können Sie den Parameter ```RESTART_WINRM=0``` zu den Installationsargumenten hinzufügen, aber WinRM muss neu gestartet werden, damit das Windows Admin Center funktioniert.

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center und automatischen Generieren eines selbstsignierten Zertifikats aus:

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center mit einem vorhandenen Zertifikat aus:

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> Das Aufrufen von `msiexec` über PowerShell mit Punkt-Schrägstrich-Notation für relative Pfade (z. B. `.\<WindowsAdminCenterInstallerName>.msi`) ist nicht möglich. Diese Notation wird nicht unterstützt, und die Installation schlägt fehl. Entfernen Sie das Präfix `.\`, oder geben Sie den vollständigen Pfad zur MSI-Datei an.

## <a name="upgrading-to-a-new-version-of-windows-admin-center"></a>Aktualisieren auf eine neue Version von Windows Admin Center

Nicht als Vorschau bereitgestellte Versionen von Windows Admin Center können mithilfe von Microsoft Update oder durch manuelle Installation aktualisiert werden.

Ihre Einstellungen werden beim Upgrade auf eine neue Version des Windows Admin Centers beibehalten. Das Upgrade der Insider Preview Versionen von Windows Admin Center werden nicht offiziell unterstützt. Es wird empfohlen, eine Neuinstallation durchzuführen, aber das Upgrade wird nicht blockiert.

## <a name="updating-the-certificate-used-by-windows-admin-center"></a>Aktualisieren des von Windows Admin Center verwendeten Zertifikats

Wenn Sie Windows Admin Center als Dienst bereitgestellt haben, müssen Sie ein Zertifikat für HTTPS bereitstellen. Um dieses Zertifikat zu einem späteren Zeitpunkt zu aktualisieren, führen Sie das Installationsprogramm erneut aus, und wählen Sie ```change``` aus.
