---
title: Installieren von Windows Admin Center
description: Windows Admin Center auf einem Windows-PC oder auf einem Server installieren, sodass mehrere Benutzer Windows Admin Center zugreifen können, die mit einem Webbrowser
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a9eb7944cd35dfa68e3c36cdc6c016f483a9f1e1
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811954"
---
# <a name="install-windows-admin-center"></a>Installieren von Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center Preview

Dieses Thema beschreibt, wie Sie Windows Admin Center auf einem Windows-PC oder auf einem Server installieren, sodass mehrere Benutzer Windows Admin Center zugreifen können, die über einen Webbrowser.

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="determine-your-installation-type"></a>Ermitteln Sie Ihren Installationstyp

Überprüfen Sie die [Installationsoptionen](../plan/installation-options.md) einschließlich der [unterstützte Betriebssysteme](../plan/installation-options.md#supported-operating-systems-installation). Zum Installieren von Windows Admin Center auf einem virtuellen Computer in Azure finden Sie unter [Deploy Windows Admin Center in Azure](../azure/deploy-wac-in-azure.md).

## <a name="install-on-windows-10"></a>Installieren unter Windows 10

Bei der Installation von Windows Admin Center auf Windows 10 wird standardmäßig Port 6516 verwendet, aber Sie haben die Möglichkeit, einen anderen Port anzugeben. Sie können auch eine Desktopverknüpfung erstellen und lassen Windows Admin Center Ihren TrustedHost verwalten.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Wenn Sie Windows Admin Center über **das Startmenü** starten, wird es in Ihrem Standardbrowser geöffnet.

Wenn Sie Windows Admin Center zum ersten Mal starten, sehen Sie ein Symbol im Benachrichtigungsbereich Ihres Desktops. Klicken Sie mit der rechten Maustaste auf dieses Symbol, und wählen Sie **Öffnen**, um das Tool in Ihrem Standardbrowser zu öffnen, oder wählen Sie **Beenden**, um den Hintergrundprozess zu beenden.

## <a name="install-on-windows-server-with-desktop-experience"></a>Installieren Sie auf Windows Server mit Desktopdarstellung

Unter Windows Server wird Windows Admin Center als Netzwerkdienst installiert. Geben Sie den Port an, den der Dienst überwacht und dies erfordert ein Zertifikat für HTTPS. Das Installationsprogramm kann zu Testzwecken ein selbstsigniertes Zertifikat erstellen, oder Sie können den Fingerabdruck eines Zertifikats bereitstellen, der bereits auf dem Computer installiert ist. Wenn Sie das generierte Zertifikat verwenden, wird es den DNS-Namen des Servers entsprechen. Wenn Sie Ihr eigenes Zertifikat verwenden, stellen Sie sicher, dass der im Zertifikat angegebene Name entspricht den Computernamen (Platzhalter, die Clientzertifikate werden nicht unterstützt.) Sie erhalten auch die Möglichkeit haben, können Ihre "TrustedHosts" Verwalten von Windows Admin Center.

> [!NOTE]
> Das Ändern von TrustedHosts ist in einer Arbeitsgruppenumgebung oder bei Verwendung von lokalen Administratoranmeldeinformationen in einer Domäne erforderlich. Wenn Sie auf diese Einstellung verzichten, müssen Sie [TrustedHosts manuell konfigurieren](../support/troubleshooting.md#configure-trustedhosts).

Sobald die Installation abgeschlossen ist, öffnen Sie einen Browser auf einem Remotecomputer, und navigieren Sie zur URL, die im letzten Schritt des Installationsprogramms angezeigt.

> [!WARNING]
> Automatisch generierte Zertifikate werden 60 Tage nach der Installation ungültig.

## <a name="install-on-server-core"></a>Installieren Sie auf Server Core

Wenn Sie über die Server Core-Installationsoption von Windows Server verfügen, können Sie Windows Admin Center über die Befehlszeile (als Administrator ausführen) installieren. Legen Sie einen Port und SSL-Zertifikat mithilfe der `SME_PORT` und `SSL_CERTIFICATE_OPTION`-Argumente fest. Wenn Sie ein vorhandenes Zertifikat verwenden, verwenden Sie `SME_THUMBPRINT`, um einen Fingerabdruck anzugeben.

> [!WARNING]
> Installieren von Windows Admin Center wird den WinRM-Dienst neu starten. alle vorangegangenen Remotesitzungen getrennt wird. Es wird empfohlen, dass Sie über eine lokale eine cmd- oder PowerShell installieren. Wenn Sie mit einem Automation-Lösung installieren, der durch den Neustart des WinRM-Diensts aufgelöst werden sollen, können Sie den Parameter hinzufügen ```RESTART_WINRM=0``` der Installation Argumente, jedoch WinRM muss neu gestartet werden für Windows Admin Center-Funktion.

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

## <a name="updating-windows-admin-center"></a>Aktualisieren von Windows Admin Center

Sie können mithilfe von Microsoft Update oder durch Manuelles Installieren von nicht-Preview-Versionen von Windows Admin Center aktualisieren. 

Die Einstellungen werden beibehalten, wenn auf eine neue Version von Windows Admin Center aktualisieren. Wird nicht offiziell unterstützt die Aktualisierung Insider Preview-Versionen von Windows Admin Center – wir glauben, dass es besser, eine saubere Installation – Sie ist, aber wir nicht blockiert.