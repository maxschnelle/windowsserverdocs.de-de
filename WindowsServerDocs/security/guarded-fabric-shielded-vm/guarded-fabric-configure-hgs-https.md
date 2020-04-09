---
title: Konfigurieren von HGS für die HTTPS-Kommunikation
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: de57a4026a33561760ad36fd78d732352b3aa340
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856843"
---
# <a name="configure-hgs-for-https-communications"></a>Konfigurieren von HGS für die HTTPS-Kommunikation

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den HGS-Server initialisieren, werden die IIS-Websites standardmäßig für die HTTP-Kommunikation konfiguriert.
Alle sensiblen Materialien, die an und von HGS übermittelt werden, werden immer mithilfe der Verschlüsselung auf Nachrichten Ebene verschlüsselt. Wenn Sie jedoch ein höheres Maß an Sicherheit wünschen, können Sie auch HTTPS aktivieren, indem Sie HGS mit einem SSL-Zertifikat konfigurieren.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

