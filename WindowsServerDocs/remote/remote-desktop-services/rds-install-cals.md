---
title: Installieren der RDS-Clientzugriffslizenzen
description: Erfahren Sie, wie Clientzugriffslizenzen für Remotedesktop-Clients zu installieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 2f283b51acc869704a52f09bebc228660cdfbc38
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870571"
---
# <a name="install-rds-client-access-licenses-on-the-remote-desktop-license-server"></a>RDS-Clientzugriffslizenzen auf dem Remotedesktop-Lizenzserver zu installieren.

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwenden Sie die folgende Informationen, um Remote Desktop Services-Clientzugriffslizenzen (CALs) auf dem Lizenzserver installieren. Nach der Installation der Clientzugriffslizenzen gibt der Lizenzserver werden Benutzern nach Bedarf.

Beachten Sie, dass Sie die Internetverbindung auf dem Computer Remotedesktoplizenzierungs-Manager ausführen, aber nicht auf dem Computer ausgeführte License Server benötigen.

1. Öffnen Sie auf dem Lizenzserver (in der Regel die erste RD-Verbindungsbroker) den Remotedesktoplizenzierungs-Manager ein.
2. Mit der rechten Maustaste des Lizenzservers, und klicken Sie dann auf **Lizenzen installieren**.
3. Klicken Sie auf **Weiter** auf der Seite Willkommen.
4. Wählen Sie das Programm, das Sie erworben haben, Ihre RDS-CALs aus, und klicken Sie dann auf **Weiter**. Wenn Sie ein Dienstanbieter sind, wählen Sie **Service Provider License Agreement**.
5. Geben Sie die Informationen für Ihre License-Programm aus. In den meisten Fällen werden die Lizenzcode oder eine Vertragsnummer, aber dies variiert abhängig von der License-Programm, das Sie verwenden.
6. Klicken Sie auf **Weiter**.
7. Wählen Sie die Version des Produkts, Lizenztyp und Anzahl der Lizenzen für Ihre Umgebung, und klicken Sie dann auf **Weiter**. Lizenzverwaltung kontaktiert das Microsoft Clearinghouse um zu überprüfen und Ihre Lizenzen abrufen.
8.  Klicken Sie auf **Fertig stellen**, um den Vorgang abzuschließen.