---
ms.assetid: cc2834ec-8f66-4209-aba3-402d710cd1bd
title: Domänencontrollersuche
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ada91f7205ba12e4d37a02e3503647c9560ccdd8
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939270"
---
# <a name="domain-controller-location"></a>Domänencontrollersuche

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Clients verwenden Domain Name System (DNS), um Domänen Controller zum Ausführen von Vorgängen wie das Verarbeiten von Anmelde Anforderungen oder das Durchsuchen des Verzeichnisses nach veröffentlichten Ressourcen zu finden. Domänen Controller registrieren eine Reihe von Datensätzen in DNS, damit Sie von Clients und anderen Computern gefunden werden. Diese Datensätze werden zusammen als Locatoreinträge bezeichnet.

Domänen Controller verwenden auch DNS, um andere Domänen Controller zu suchen und Aufgaben wie die Replikation auszuführen. Der Prozess, mit dem Domänen Controller nach anderen Domänen Controllern suchen, ist identisch mit dem Prozess, mit dem Clients Domänen Controller suchen.



