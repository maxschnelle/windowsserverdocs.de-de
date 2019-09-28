---
title: Konfigurieren von HGS für die HTTPS-Kommunikation
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f0cbf6a6dc1970499758a6a48bfaadb95c464ec1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403680"
---
# <a name="configure-hgs-for-https-communications"></a>Konfigurieren von HGS für die HTTPS-Kommunikation

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den HGS-Server initialisieren, werden die IIS-Websites standardmäßig für die HTTP-Kommunikation konfiguriert.
Alle sensiblen Materialien, die an und von HGS übermittelt werden, werden immer mithilfe der Verschlüsselung auf Nachrichten Ebene verschlüsselt. Wenn Sie jedoch ein höheres Maß an Sicherheit wünschen, können Sie auch HTTPS aktivieren, indem Sie HGS mit einem SSL-Zertifikat konfigurieren.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

