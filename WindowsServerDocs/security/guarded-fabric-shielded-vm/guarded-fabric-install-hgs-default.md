---
title: Installieren von HGS in einer neuen Gesamtstruktur
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: c18c14435c93d08c98b1a765fd820294a273a575
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939544"
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


