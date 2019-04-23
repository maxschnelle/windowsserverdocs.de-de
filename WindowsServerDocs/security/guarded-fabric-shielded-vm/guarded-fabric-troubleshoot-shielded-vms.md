---
title: Problembehandlung für abgeschirmte VMs
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/3/2018
ms.openlocfilehash: 13ff0dad1519d394ce74a91efbfcc9e2f237e4a5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850031"
---
# <a name="troubleshoot-shielded-vms"></a>Problembehandlung für abgeschirmte VMs

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Ab Windows Server-Version 1803 sind "Erweiterte Sitzung" Verbindung mit virtuellen Computern (VMConnect) und PS direkt aktiviert werden, damit vollständig abgeschirmte VMs. Der Virtualization Admin erfordert weiterhin die VM-Gast-Anmeldeinformationen für den Zugriff auf den virtuellen Computer, aber dies erleichtert es für einen Hoster eine abgeschirmte VM beheben, wenn die Netzwerkkonfiguration unterbrochen wurde.

Um VMConnect und PS direkt für die abgeschirmten VMs aktivieren möchten, verschieben Sie sie einfach auf einen Hyper-V-Host, der Windows Server-Version 1803 oder höher ausgeführt wird. Der virtuellen Geräte, sodass für diese Funktionen werden automatisch wieder aktiviert werden. Wenn eine abgeschirmte VM, die auf einen Host, der ausgeführt wird und die frühere Version von Windows Server verschoben wird, wird VMConnect und PS Direct wieder deaktiviert werden.

Sicherheitsrelevante-Kunden, die Sorge, wenn Hoster haben Zugriff auf den virtuellen Computer und zum ursprünglichen Verhalten zurückzukehren möchten, sollten die folgenden Funktionen im Gastbetriebssystem deaktiviert werden:

- Deaktivieren Sie die PowerShell Direct-Dienst auf dem virtuellen Computer:

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- VMConnect erweiterte Sitzungsmodus kann nur deaktiviert werden, ob Ihr Gastbetriebssystem mindestens Windows Server-2019 oder Windows 10, Version 1809. Fügen Sie den folgenden Registrierungsschlüssel auf dem virtuellen Computer, um konsolenverbindungen VMConnect erweiterte Sitzung zu deaktivieren:

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
