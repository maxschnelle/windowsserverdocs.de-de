---
title: 'Remotedesktopdienste: Ausrichten auf verschiedene Arten von Benutzern'
description: In diesem Artikel werden die verschiedenen Arten von Benutzern für die Remotedesktopdienste beschrieben.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da522a18-c33f-468e-b9d6-3ad7d3cfba26
author: spatnaik
ms.author: spatnaik
ms.date: 11/06/2019
manager: scottman
ms.openlocfilehash: dc83d76dbfaded9dadae7c16ae9e1c8df7958a7d
ms.sourcegitcommit: d25e47a54a120b9bc26ff43597518fca58c1cc5b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753827"
---
# <a name="remote-desktop-services---cater-to-different-kinds-of-users"></a>Remotedesktopdienste: Ausrichten auf verschiedene Arten von Benutzern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Remotedesktopdienste unterstützen unterschiedliche Typen von Arbeitsauslastungen. Skaliere deine Bereitstellung je nach den erwarteten Anforderungen jedes Benutzertyps.

## <a name="types-of-users"></a>Benutzertypen

### <a name="knowledge-user"></a>Wissensbenutzer

Wissensbenutzer verwenden einfache Produktivitätsanwendungen wie Microsoft Word, Excel, Outlook und den Microsoft Edge-Browser.

Wissensbenutzern wird empfohlen, nicht mehr als vier Benutzer pro virtueller CPU (vCPU) zu verwenden.

### <a name="professional-user"></a>Professionelle Benutzer

Professionelle Benutzer verwenden Internetbrowser und Produktivitätsanwendungen zusätzlich zur Unterstützung von intensiveren Arbeitsauslastungen wie der Softwareentwicklung und der Erstellung von Multimedia-Inhalten.

Für professionelle Benutzer werden maximal zwei Benutzer pro vCPU empfohlen.

### <a name="power-user"></a>Poweruser

Poweruser verwenden Engineering- und Grafikanwendungen wie Programme für computergestütztes Design (CAD) und Adobe Photoshop. GPUs sind häufig eine gute Wahl für Benutzer, die regelmäßig grafikintensive Programme zum Rendern von Videos, für 3D-Entwürfe und für Simulationen verwenden.

Powerusern sollten nicht mehr als einen Benutzer pro vCPU verwenden.

Weitere Informationen zur Grafikbeschleunigung findest du unter [Auswählen der Grafikrenderingtechnologie](rds-graphics-virtualization.md).

Azure bietet andere Bereitstellungsoptionen für Grafikbeschleunigung sowie mehrere verfügbare GPU-VM-Größen. Weitere Informationen dazu findest du unter [Für GPU optimierte VM-Größen](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).

## <a name="test-workload"></a>Testen der Arbeitsauslastung

Es wird empfohlen, Testbereitstellungen zu laden, die sowohl Belastungstests als auch Echtzeit-Anwendungssimulationen umfassten. Auch mit Simulationstools kannst du Auslastungstest deiner Bereitstellung durchführen. Stelle sicher, dass das System reaktionsfähig und robust genug ist, um die Benutzeranforderungen zu erfüllen, und denke daran, die Ladegröße zu verändern, um böse Überraschungen zu vermeiden.
