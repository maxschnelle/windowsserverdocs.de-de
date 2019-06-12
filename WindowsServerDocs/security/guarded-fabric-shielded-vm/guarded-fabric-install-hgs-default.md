---
title: Host-Überwachungsdienst in einer neuen Gesamtstruktur installieren
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 84f88d96f1e16767dec3b21b34aa226e544afaac
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447406"
---
# <a name="install-hgs-in-a-new-forest"></a>Host-Überwachungsdienst in einer neuen Gesamtstruktur installieren 

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

## <a name="add-the-hgs-server-role"></a>Fügen Sie die Host-Überwachungsdienst-Serverrolle hinzu.

Führen Sie die folgenden Befehle in einer mit erhöhten Rechten PowerShell-Sitzung den HGS-Server-Rolle hinzufügen, und installieren die Host-Überwachungsdienst.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>Installieren von HGS 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>Nächste Schritte

- Die nächsten Schritte zum Einrichten von TPM-basierten Nachweis, finden Sie unter [initialisiert den Host-Überwachungsdienst-Cluster mithilfe von TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-tpm-mode-default.md).
- Die nächsten Schritte, um den schlüsselnachweis Host einzurichten, finden Sie unter [initialisiert den Host-Überwachungsdienst-Cluster mithilfe von Schlüssel-Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-key-mode-default.md).
- Für die nächsten Schritte zum Einrichten der Admin-basierten nachweisen (in Windows Server-2019 veraltet) finden Sie unter [initialisiert den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-ad-mode-default.md).

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Initialisieren von HGS](guarded-fabric-initialize-hgs.md)


