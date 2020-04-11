---
title: Der Remotelaptop trennt die WLAN-Verbindung
description: Beheben eines Problems, bei dem der Remotelaptop die Verbindung mit dem Drahtlosnetzwerk trennt.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 72bf482512ff3bb0a678ae59cd6ac20b947a54d9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857153"
---
# <a name="remote-laptop-disconnects-from-wireless-network"></a>Der Remotelaptop trennt die WLAN-Verbindung

Dieses Problem kann auftreten, wenn ein Remotedesktopclient eine Verbindung mit einem Laptopcomputer über ein 802.1x-Drahtlosnetzwerk herstellt. Gelegentlich trennt der Laptop die Verbindung mit dem Drahtlosnetzwerk, ohne sie automatisch wiederherzustellen.

Dies ist ein bekanntes Problem, das auftritt, wenn die Netzwerk-Authentifizierungseinstellung für die drahtlose Netzwerkverbindung **Benutzerauthentifizierung** ist.

Um dieses Problem zu umgehen, legen Sie Netzwerk-Authentifizierungseinstellung auf **Benutzer- oder Computerauthentifizierung** oder auf **Computerauthentifizierung** fest.

 > [!NOTE]  
> Um die Netzwerk-Authentifizierungseinstellungen auf einem einzelnen Computer zu ändern, müssen Sie möglicherweise die Systemsteuerung im Netzwerk- und Freigabecenter verwenden, um eine neue Drahtlosverbindung mit den neuen Einstellungen zu erstellen.

Eine vollständige Beschreibung der Konfiguration von Netzwerkeinstellungen mithilfe von Gruppenrichtlinienobjekten finden Sie unter [Configure Wireless Network (IEEE 802.11) Policies](../../../networking/core-network-guide/cncg/wireless/e-wireless-access-deployment.md#bkmk_policies) (Konfigurieren von Richtlinien für Drahtlosnetzwerke (IEEE 802.11)).
