---
title: Installieren von HGS in einer neuen Gesamtstruktur
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8f896b0cea49f9dd26a828a2580b59a78348763a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856603"
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


