---
title: Installieren von HGS in einer neuen Gesamtstruktur
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 6dfbe24fb4d9011b48f366d7e5df92fdb80685d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386589"
---
# <a name="install-hgs-in-a-new-forest"></a>Installieren von HGS in einer neuen Gesamtstruktur 

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

## <a name="add-the-hgs-server-role"></a>Hinzufügen der HGS-Server Rolle

Führen Sie die folgenden Befehle in einer PowerShell-Sitzung mit erhöhten Rechten aus, um die HGS-Server Rolle hinzufügen und HGS installieren.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>Installieren von HGS 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>Nächste Schritte

- Die nächsten Schritte zum Einrichten eines TPM-basierten Nachweis finden Sie unter [Initialisieren des HGS-Clusters mit dem TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-tpm-mode-default.md).
- Die nächsten Schritte zum Einrichten des Host Schlüssel-Attestation finden Sie unter [Initialisieren des HGS-Clusters mithilfe des Schlüssel Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-key-mode-default.md).
- Die nächsten Schritte zum Einrichten des Administrator basierten Nachweis (veraltet in Windows Server 2019) finden Sie unter [Initialisieren des HGS-Clusters mit dem AD-Modus in einer neuen dedizierten Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-ad-mode-default.md).

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Initialisieren von HGS](guarded-fabric-initialize-hgs.md)


