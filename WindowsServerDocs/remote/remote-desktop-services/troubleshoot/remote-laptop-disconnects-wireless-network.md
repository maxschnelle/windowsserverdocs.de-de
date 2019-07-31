---
title: Der Remotelaptop trennt die WLAN-Verbindung
description: Beheben eines Problems, bei dem der Remotelaptop die Verbindung mit dem Drahtlosnetzwerk trennt.
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: ''
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 70aaad61cf068fe38fa95127700655db2a186dd1
ms.sourcegitcommit: f6503e503d8f08ba8000db9c5eda890551d4db37
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68529870"
---
# <a name="remote-laptop-disconnects-from-wireless-network"></a>Der Remotelaptop trennt die WLAN-Verbindung

Dieses Problem kann auftreten, wenn ein Remotedesktopclient eine Verbindung mit einem Laptopcomputer über ein 802.1x-Drahtlosnetzwerk herstellt. Gelegentlich trennt der Laptop die Verbindung mit dem Drahtlosnetzwerk, ohne sie automatisch wiederherzustellen.

Dies ist ein bekanntes Problem, das auftritt, wenn die Netzwerk-Authentifizierungseinstellung für die drahtlose Netzwerkverbindung **Benutzerauthentifizierung** ist.

Um dieses Problem zu umgehen, legen Sie Netzwerk-Authentifizierungseinstellung auf **Benutzer- oder Computerauthentifizierung** oder auf **Computerauthentifizierung** fest.

 > [!NOTE]  
> Um die Netzwerk-Authentifizierungseinstellungen auf einem einzelnen Computer zu ändern, müssen Sie möglicherweise die Systemsteuerung im Netzwerk- und Freigabecenter verwenden, um eine neue Drahtlosverbindung mit den neuen Einstellungen zu erstellen.

Eine vollständige Beschreibung der Konfiguration von Netzwerkeinstellungen mithilfe von Gruppenrichtlinienobjekten finden Sie unter [Configure Wireless Network (IEEE 802.11) Policies](../../../networking/core-network-guide/cncg/wireless/e-wireless-access-deployment.md#bkmk_policies) (Konfigurieren von Richtlinien für Drahtlosnetzwerke (IEEE 802.11)).
