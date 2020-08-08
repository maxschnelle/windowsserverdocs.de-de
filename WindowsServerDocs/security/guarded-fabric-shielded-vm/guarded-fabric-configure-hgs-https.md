---
title: Konfigurieren von HGS für die HTTPS-Kommunikation
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 4e708b61bd629b5b784926338b1aee122e2ecbee
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966157"
---
# <a name="configure-hgs-for-https-communications"></a>Konfigurieren von HGS für die HTTPS-Kommunikation

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den HGS-Server initialisieren, werden die IIS-Websites standardmäßig für die HTTP-Kommunikation konfiguriert.
Alle sensiblen Materialien, die an und von HGS übermittelt werden, werden immer mithilfe der Verschlüsselung auf Nachrichten Ebene verschlüsselt. Wenn Sie jedoch ein höheres Maß an Sicherheit wünschen, können Sie auch HTTPS aktivieren, indem Sie HGS mit einem SSL-Zertifikat konfigurieren.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)]

