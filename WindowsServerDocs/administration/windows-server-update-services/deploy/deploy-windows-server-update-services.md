---
title: Bereitstellen von Windows Server Update Services
description: Windows Server Update Service (WSUS)-Thema – eine Übersicht über den Bereitstellungsprozess mit Links zu den vier Schritten dorthin
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: get-started-article
ms.assetid: 2708f6b2-4252-4b8f-9b7e-84c9b4222075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51972ad352f6530c8ee2aa84aec57b62784da728
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873181"
---
# <a name="deploy-windows-server-update-services"></a>Bereitstellen von Windows Server Update Services

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Windows Server Update Services (WSUS) ermöglicht IT-Administratoren das Bereitstellen der aktuellen Microsoft-Produktupdates. WSUS ist eine Windows Server-Serverrolle, die zum Verwalten und Verteilen von Updates installiert werden kann. Ein WSUS-Server kann als Updatequelle für andere WSUS-Server in der Organisation dienen. Der als Updatequelle eingesetzte WSUS-Server wird als Upstreamserver bezeichnet.  

In einer WSUS-Implementierung muss mindestens ein WSUS-Server im Netzwerk eine Verbindung mit Microsoft Update herstellen, um verfügbare Updateinformationen herunterzuladen. Sie können feststellen, basierend auf der Netzwerksicherheit und Konfiguration, wie viele andere Server direkt Herstellen einer Verbindung mit Microsoft Update.  

Dieses Handbuch enthält grundlegende Informationen zum Planen und Bereitstellen von Windows Server Update Services.  

-   [Planen der WSUS-Bereitstellung](../plan/plan-your-wsus-deployment.md)  

-   [Schritt 1: Installieren der WSUS-Serverrolle](1-install-the-wsus-server-role.md)  

-   [Schritt 2: Konfigurieren von WSUS](2-configure-wsus.md)  

-   [Schritt 3: Genehmigen und Bereitstellen von Updates in WSUS](3-approve-and-deploy-updates-in-wsus.md)  

-   [Schritt 4: Konfigurieren der Gruppenrichtlinieneinstellungen für automatische Updates](4-configure-group-policy-settings-for-automatic-updates.md)  
