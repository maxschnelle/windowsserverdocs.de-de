---
title: NPS-Vorlagen
description: Dieses Thema bietet einen Überblick über die Netzwerk Richtlinien Server-Vorlagen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bafff7a6a15312ab1bdca2e7b98307bc94731d3a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405312"
---
# <a name="nps-templates"></a>NPS-Vorlagen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mithilfe von Netzwerk Richtlinien Server-\(NPS-\) Vorlagen können Sie Konfigurationselemente erstellen, z. b. Remote Authentication Dial-in User Service \(RADIUS\) Clients oder gemeinsame geheime Schlüssel, die Sie auf dem lokalen NPS wieder verwenden und für die Verwendung auf anderen NPSS verwenden können.

NPS-Vorlagen sind so konzipiert, dass der Zeit-und Kostenaufwand für die Konfiguration von NPS auf einem oder mehreren Servern reduziert wird. Die folgenden NPS-Vorlagen Typen sind für die Konfiguration in der Vorlagen Verwaltung verfügbar:

- Gemeinsame geheime Schlüssel
- RADIUS-Clients
- Remote-RADIUS-Server
- IP-Filter
- Wiederherstellungs Server Gruppen

Das Konfigurieren einer Vorlage unterscheidet sich von der direkten Konfiguration des NPS. Das Erstellen einer Vorlage wirkt sich nicht auf die Funktionalität von NPS aus. Dies ist nur der Fall, wenn Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen, dass die Vorlage die NPS-Funktionalität beeinträchtigt. 

Wenn Sie z. b. einen RADIUS-Client in der NPS-Konsole unter RADIUS-Clients und-Server konfigurieren, haben Sie die NPS-Konfiguration geändert und einen Schritt zum Konfigurieren von NPS für die Kommunikation mit einem Ihrer Netzwerk Zugriffs Server \(NAS-\)vorgenommen. \(der nächste Schritt besteht darin, den NAS für die Kommunikation mit NPS zu konfigurieren. Wenn Sie jedoch eine neue RADIUS-Client Vorlage in der NPS-Konsole unter **Vorlagen Verwaltung** konfigurieren, anstatt einen neuen RADIUS-Client unter **RADIUS-Clients und-Server zu**erstellen, haben Sie eine Vorlage erstellt, aber Sie haben die NPS-Funktionalität noch nicht geändert.\) Um die NPS-Funktionalität zu ändern, müssen Sie die Vorlage am richtigen Speicherort in der NPS-Konsole auswählen.

## <a name="creating-templates"></a>Erstellen von Vorlagen

Öffnen Sie zum Erstellen einer Vorlage die NPS-Konsole, klicken Sie mit der rechten Maustaste auf einen Vorlagentyp, z. b. **IP-Filter**, und klicken Sie dann auf **neu** Das Dialogfeld neue Vorlagen Eigenschaften wird geöffnet, in dem Sie die Vorlage konfigurieren können.

## <a name="using-templates-locally"></a>Lokales Verwenden von Vorlagen

Sie können eine Vorlage verwenden, die Sie in der **Vorlagen Verwaltung** erstellt haben, indem Sie zu einem Speicherort in der NPS-Konsole navigieren, an dem die Vorlage angewendet werden kann. Wenn Sie z. b. eine neue Vorlage für freigegebene Geheimnisse erstellen, die Sie auf eine RADIUS-Client Konfiguration anwenden möchten, öffnen Sie in **RADIUS-Clients und-Server** und **RADIUS-Clients**die Eigenschaften des RADIUS-Clients. Wählen Sie unter **vorhandene freigegebene**geheime Schlüssel auswählen die Vorlage aus, die Sie zuvor in der Liste der verfügbaren Vorlagen erstellt haben.

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
