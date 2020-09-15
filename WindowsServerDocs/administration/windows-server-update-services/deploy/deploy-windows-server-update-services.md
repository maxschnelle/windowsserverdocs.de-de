---
title: Bereitstellen von Windows Server Update Services
description: 'Artikel zu Windows Server Update Services (WSUS): Übersicht über den Bereitstellungsprozess mit Links zu den vier Schritten der Vorgehensweise'
ms.topic: get-started-article
ms.assetid: 2708f6b2-4252-4b8f-9b7e-84c9b4222075
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 78df9b93205e07e58310ad2077571b29b9ff5360
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624546"
---
# <a name="deploy-windows-server-update-services"></a>Bereitstellen von Windows Server Update Services

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server Update Services (WSUS) ermöglicht IT-Administratoren das Bereitstellen der aktuellen Microsoft-Produktupdates. WSUS ist eine Windows Server-Serverrolle, die zum Verwalten und Verteilen von Updates installiert werden kann. Ein WSUS-Server kann als Updatequelle für andere WSUS-Server in der Organisation dienen. Der als Updatequelle eingesetzte WSUS-Server wird als Upstreamserver bezeichnet.

In einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk eine Verbindung mit Microsoft Update herstellen, um verfügbare Updateinformationen herunterzuladen. Sie können basierend auf der Netzwerksicherheit und -konfiguration festlegen, wie viele weitere Server eine direkte Verbindung mit Microsoft Update herstellen.

In diesem Leitfaden erhalten Sie grundlegende Informationen zur Planung und Bereitstellung von Windows Server Update Services.

-   [Planen der WSUS-Bereitstellung](../plan/plan-your-wsus-deployment.md)

-   [Schritt 1: Installieren Sie die WSUS-Serverrolle](1-install-the-wsus-server-role.md)

-   [Schritt 2: Konfigurieren von WSUS](2-configure-wsus.md)

-   [Schritt 3: Genehmigen und Bereitstellen von Updates in WSUS](3-approve-and-deploy-updates-in-wsus.md)

-   [Schritt 4: Konfigurieren von Gruppenrichtlinien für automatische Updates](4-configure-group-policy-settings-for-automatic-updates.md)
