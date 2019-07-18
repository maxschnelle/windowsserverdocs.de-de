---
title: Installieren von Windows Admin Center
description: Installieren des Windows Admin Centers auf einem Windows-PC oder auf einem Server, sodass mehrere Benutzer mithilfe eines Webbrowsers auf das Windows Admin Center zugreifen können.
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 994e2324042dd441abbb114da2b8806574ce0352
ms.sourcegitcommit: e5553285d509f15c20ba98ad9e8bf69b09531560
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68307485"
---
# <a name="install-windows-admin-center"></a>Installieren von Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Thema wird beschrieben, wie Sie das Windows Admin Center auf einem Windows-PC oder auf einem Server installieren, damit mehrere Benutzer über einen Webbrowser auf das Windows Admin Center zugreifen können.

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="determine-your-installation-type"></a>Bestimmen des Installations Typs

Überprüfen Sie die [Installationsoptionen](../plan/installation-options.md) , einschließlich der [unterstützten Betriebssysteme](../plan/installation-options.md#supported-operating-systems-installation). Informationen zum Installieren des Windows Admin Centers auf einem virtuellen Computer in Azure finden Sie unter Bereitstellen [des Windows Admin Centers in Azure](../azure/deploy-wac-in-azure.md).

## <a name="install-on-windows-10"></a>Installieren unter Windows 10

Bei der Installation von Windows Admin Center auf Windows 10 wird standardmäßig Port 6516 verwendet, aber Sie haben die Möglichkeit, einen anderen Port anzugeben. Sie können auch eine Desktopverknüpfung erstellen und lassen Windows Admin Center Ihren TrustedHost verwalten.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Wenn Sie Windows Admin Center über **das Startmenü** starten, wird es in Ihrem Standardbrowser geöffnet.

Wenn Sie Windows Admin Center zum ersten Mal starten, sehen Sie ein Symbol im Benachrichtigungsbereich Ihres Desktops. Klicken Sie mit der rechten Maustaste auf dieses Symbol, und wählen Sie **Öffnen**, um das Tool in Ihrem Standardbrowser zu öffnen, oder wählen Sie **Beenden**, um den Hintergrundprozess zu beenden.

## <a name="install-on-windows-server-with-desktop-experience"></a>Installieren Sie auf Windows Server mit Desktopdarstellung

Unter Windows Server wird Windows Admin Center als Netzwerkdienst installiert. Geben Sie den Port an, den der Dienst überwacht und dies erfordert ein Zertifikat für HTTPS. Das Installationsprogramm kann zu Testzwecken ein selbstsigniertes Zertifikat erstellen, oder Sie können den Fingerabdruck eines Zertifikats bereitstellen, der bereits auf dem Computer installiert ist. Wenn Sie das generierte Zertifikat verwenden, wird es den DNS-Namen des Servers entsprechen. Wenn Sie Ihr eigenes Zertifikat verwenden, stellen Sie sicher, dass der im Zertifikat angegebene Name mit dem Computernamen übereinstimmt (Platzhalter Zertifikate werden nicht unterstützt). Sie haben auch die Möglichkeit, das Windows Admin Center zum Verwalten Ihrer Treuhänder Hosts zu verwenden.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Öffnen Sie nach Abschluss der Installation einen Browser von einem Remote Computer aus, und navigieren Sie zu der URL, die Sie im letzten Schritt des Installers angezeigt haben.

> [!WARNING]
> Automatisch generierte Zertifikate werden 60 Tage nach der Installation ungültig.

## <a name="install-on-server-core"></a>Installieren Sie auf Server Core

Wenn Sie über die Server Core-Installationsoption von Windows Server verfügen, können Sie Windows Admin Center über die Befehlszeile (als Administrator ausführen) installieren. Legen Sie einen Port und SSL-Zertifikat mithilfe der `SME_PORT` und `SSL_CERTIFICATE_OPTION`-Argumente fest. Wenn Sie ein vorhandenes Zertifikat verwenden, verwenden Sie `SME_THUMBPRINT`, um einen Fingerabdruck anzugeben.

> [!WARNING]
> Beim Installieren von Windows Admin Center wird der WinRM-Dienst neu gestartet, wodurch alle remotepowershells-Sitzungen abgewartet werden. Es wird empfohlen, dass Sie über eine lokale cmd oder PowerShell installieren. Wenn Sie die Installation mit einer Automatisierungslösung durchführt, die vom WinRM-Dienst neu gestartet wird, können Sie den- ```RESTART_WINRM=0``` Parameter den Installations Argumenten hinzufügen, aber WinRM muss neu gestartet werden, damit das Windows Admin Center funktioniert.

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center aus und um automatisch ein selbstsigniertes Zertifikat zu generieren:

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

Führen Sie den folgenden Befehl zum Installieren von Windows Admin Center mit einem vorhandenen Zertifikat aus:

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> Das Aufrufen von `msiexec` über PowerShell mit Punkt-Schrägstrich-Notation für relative Pfade (z. B. `.\<WindowsAdminCenterInstallerName>.msi`) ist nicht möglich. Diese Notation wird nicht unterstützt, und die Installation schlägt fehl. Entfernen Sie das Präfix `.\` oder geben Sie den vollständigen Pfad zur MSI-Datei an.

## <a name="upgrading-to-a-new-version-of-windows-admin-center"></a>Aktualisieren auf eine neue Version von Windows Admin Center

Nicht als Vorschau bereitgestellte Versionen von Windows Admin Center können mithilfe von Microsoft Update oder durch manuelle Installation aktualisiert werden.

Ihre Einstellungen werden bei einem Upgrade auf eine neue Version des Windows Admin Centers beibehalten. Wir unterstützen nicht offiziell das Upgrade der Insider-Vorschau Versionen von Windows Admin Center. wir denken, es ist besser, eine saubere Installation durchzuführen, aber wir blockieren Sie nicht.

## <a name="updating-the-certificate-used-by-windows-admin-center"></a>Aktualisieren des vom Windows Admin Center verwendeten Zertifikats

Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben, müssen Sie ein Zertifikat für HTTPS bereitstellen. Führen Sie das Installationsprogramm erneut aus, und wählen Sie ```change```aus, um dieses Zertifikat zu einem späteren Zeitpunkt zu aktualisieren.
