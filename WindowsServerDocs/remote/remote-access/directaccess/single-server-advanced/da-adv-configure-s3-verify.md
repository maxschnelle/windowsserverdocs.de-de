---
title: Schritt 3 Überprüfen der erweiterten DirectAccess-Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ae8bbff0-c981-4bc6-8df1-861621d0627f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3d5b189d70497ead26f24f43bba9dcfe2d443ce0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989759"
---
# <a name="step-3-verify-the-advanced-directaccess-deployment"></a>Schritt 3 Überprüfen der erweiterten DirectAccess-Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob Sie die DirectAccess-Bereitstellung ordnungsgemäß konfiguriert haben

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>So überprüfen Sie den Zugriff auf interne Ressourcen über DirectAccess

1.  Verbinden eines DirectAccess-Client Computers mit dem Unternehmensnetzwerk und Abrufen des Gruppenrichtlinie Objekts.

2.  Klicken Sie im Benachrichtigungsbereich auf das Symbol **Netzwerkverbindungen** , um auf den DirectAccess-Medien-Manager zuzugreifen.

3.  Klicken Sie auf **DirectAccess-Verbindung**, und Sie werden feststellen, dass der Status **Lokal verbunden**ist.

4.  Verbinden Sie des Clientcomputers mit dem externen Netzwerk ein, und versuchen Sie den Zugriff auf interne Ressourcen.

    Sie sollten auf alle Unternehmensressourcen zugreifen können.

## <a name="previous-step"></a><a name="BKMK_Links"></a>Vorheriger Schritt

-   [Schritt 2: Konfigurieren von DirectAccess-Servern](./da-adv-configure-s2-servers.md)