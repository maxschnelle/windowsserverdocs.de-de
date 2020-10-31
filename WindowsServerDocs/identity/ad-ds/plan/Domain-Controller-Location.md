---
ms.assetid: cc2834ec-8f66-4209-aba3-402d710cd1bd
title: Domänencontrollersuche
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d22abba814d9cd4b18294b3c54d550b28c2dfef5
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068722"
---
# <a name="domain-controller-location"></a>Domänencontrollersuche

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Clients verwenden Domain Name System (DNS), um Domänen Controller zum Ausführen von Vorgängen wie das Verarbeiten von Anmelde Anforderungen oder das Durchsuchen des Verzeichnisses nach veröffentlichten Ressourcen zu finden. Domänen Controller registrieren eine Reihe von Datensätzen in DNS, damit Sie von Clients und anderen Computern gefunden werden. Diese Datensätze werden zusammen als Locatoreinträge bezeichnet.

Domänen Controller verwenden auch DNS, um andere Domänen Controller zu suchen und Aufgaben wie die Replikation auszuführen. Der Prozess, mit dem Domänen Controller nach anderen Domänen Controllern suchen, ist identisch mit dem Prozess, mit dem Clients Domänen Controller suchen.



