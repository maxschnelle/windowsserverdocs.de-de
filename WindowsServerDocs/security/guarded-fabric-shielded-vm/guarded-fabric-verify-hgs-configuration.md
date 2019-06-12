---
title: Überprüfen der HGS-Konfiguration
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 954393126333bf04d2aa46a01089d88bc91151cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447324"
---
# <a name="verify-the-hgs-configuration"></a>Überprüfen der HGS-Konfiguration

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Als Nächstes müssen wir überprüfen, dass alles wie erwartet funktioniert. Zu diesem Zweck führen Sie den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten aus:

```powershell
Get-HgsTrace -RunDiagnostics
```

Da die Host-Überwachungsdienst-Konfiguration keine noch Informationen zu den Hosts, die in geschützten Fabrics werden enthält, gibt die Diagnose, dass keine Hosts erfolgreich noch bestätigen können. Ignorieren Sie dieses Ergebnis zu, und überprüfen Sie die anderen Informationen, die von der Diagnose bereitgestellt.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

<!-- When a link is available for an updated troubleshooting guide, add a sentence like the following and create a link to the troubleshooting guide:
If failures did occur, please review the remediation steps provided or see the Troubleshooting Guide.
-->

Führen Sie die Diagnose auf jedem Knoten im Cluster-Host-Überwachungsdienst.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bereitstellen geschützter Hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

