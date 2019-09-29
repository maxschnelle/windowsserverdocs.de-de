---
title: Überprüfen der HGS-Konfiguration
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: d219b7aa9ca1e17df3281fd756106a6f07864116
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386351"
---
# <a name="verify-the-hgs-configuration"></a>Überprüfen der HGS-Konfiguration

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016


Als nächstes müssen wir überprüfen, ob die Dinge erwartungsgemäß funktionieren. Führen Sie hierzu den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten aus:

```powershell
Get-HgsTrace -RunDiagnostics
```

Da die HGS-Konfiguration noch keine Informationen zu den Hosts enthält, die im geschützten Fabric enthalten sein werden, weist die Diagnose darauf hin, dass noch keine Hosts erfolgreich bestätigt werden können. Ignorieren Sie dieses Ergebnis, und überprüfen Sie die anderen von der Diagnose bereitgestellten Informationen.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

Führen Sie die Diagnose auf jedem Knoten in Ihrem HGS-Cluster aus.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bereitstellen geschützter Hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

