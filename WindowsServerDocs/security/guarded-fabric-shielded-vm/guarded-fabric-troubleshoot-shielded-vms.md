---
title: Problembehandlung bei abgeschirmten VMS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 10/3/2018
ms.openlocfilehash: 6bcc32aae736a927576de28a15ca532279d4753b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944010"
---
# <a name="troubleshoot-shielded-vms"></a>Problembehandlung bei abgeschirmten VMS

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Ab Windows Server Version 1803 werden der erweiterte Sitzungs Modus (Virtual Machine Connection, VMConnect) und PS Direct für vollständig abgeschirmte VMS erneut aktiviert. Der Virtualisierungsadministrator benötigt trotzdem VM-Gast Anmelde Informationen, um Zugriff auf den virtuellen Computer zu erhalten. Dadurch wird es für einen Host jedoch einfacher, Probleme mit einer abgeschirmten VM zu beheben, wenn die Netzwerkkonfiguration beschädigt ist.

Um VMConnect und PS Direct für Ihre abgeschirmten VMS zu aktivieren, verschieben Sie Sie einfach auf einen Hyper-V-Host, auf dem Windows Server, Version 1803 oder höher, ausgeführt wird. Die virtuellen Geräte, die diese Features zulassen, werden automatisch erneut aktiviert. Wenn eine abgeschirmte VM auf einen Host verschoben wird, auf dem und eine frühere Version von Windows Server ausgeführt wird, werden VMConnect und PS Direct erneut deaktiviert.

Für sicherheitsrelevante Kunden, die sich Gedanken darüber machen, ob Hoster Zugriff auf die VM haben und zum ursprünglichen Verhalten zurückkehren möchten, sollten die folgenden Funktionen im Gast Betriebssystem deaktiviert werden:

- Deaktivieren Sie den PowerShell Direct-Dienst auf dem virtuellen Computer:

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- Der erweiterte VMConnect-Sitzungs Modus kann nur deaktiviert werden, wenn Ihr Gast Betriebssystem mindestens Windows Server 2019 oder Windows 10, Version 1809, entspricht. Fügen Sie den folgenden Registrierungsschlüssel in Ihrem virtuellen Computer hinzu, um VMConnect-Verbindungen mit erweiterten Sitzungs Konsolen zu deaktivieren:

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
