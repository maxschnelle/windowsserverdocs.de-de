---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: d1bfc74c4daa751e3081b26c87dd0d2c88f5f095
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879851"
---
Die Optionen für die Standby-Adapter sind **keine (alle Adapter aktiv)** oder Ihre Auswahl für einen bestimmten Netzwerkadapter im NIC-Team, die als Standby-Adapter dient. Wenn Sie eine NIC als Standby-Adapter konfigurieren, alle nicht ausgewählten Teammitglieder sind aktiv, und kein Netzwerkdatenverkehr gesendet bzw. vom Adapter verarbeitet werden, bis eine aktive NIC fehlschlägt. Wenn eine aktive NIC fehlgeschlagen ist, die Standby-NIC aktiviert wird und der Netzwerkdatenverkehr für Prozesse. Wenn alle Teammitglieder Dienst wiederhergestellt zu erhalten, wird das standby-Team-Element zu standby-Status zurückgegeben.  