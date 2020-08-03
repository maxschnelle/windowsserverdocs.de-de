---
title: Schritt 3 Überprüfen der Remote Zugriffs Bereitstellung (VPN)
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 43ac612e-2e77-418c-8171-ebb2086b7cb6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9eb64024eb7ad9b80a1ba8c949939b33426ad6da
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87518156"
---
# <a name="step-3-verify-the-remote-access-vpn-deployment"></a>Schritt 3 Überprüfen der Remote Zugriffs Bereitstellung (VPN)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob Sie die DirectAccess-Bereitstellung ordnungsgemäß konfiguriert haben

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>So überprüfen Sie den Zugriff auf interne Ressourcen über DirectAccess

1.  Einen DirectAccess-Client-Computer mit dem Unternehmensnetzwerk herstellen und die Gruppenrichtlinie zu erhalten.

2.  Klicken Sie auf die**Netzwerkverbindungen**-Symbol im Infobereich angezeigt, DA Medien-Manager zugreifen.

3.  Klicken Sie auf die**DirectAccess-Verbindung**und Sie sehen, dass der Status**lokal verbundenen**.

4.  Verbinden Sie des Clientcomputers mit dem externen Netzwerk ein, und versuchen Sie den Zugriff auf interne Ressourcen.

    Sie sollten auf alle Unternehmensressourcen zugreifen können.



