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
ms.date: 09/23/2016
manager: scottman
ms.openlocfilehash: c04909e9e0cfbf71b6632c154ac8b9b20b5bac10
ms.sourcegitcommit: b4b0e73ce35f8b594eb467a2bb2aa91bd6d86369
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2019
ms.locfileid: "72893075"
---
# <a name="remote-desktop-services---cater-to-different-kinds-of-users"></a>Remotedesktopdienste: Ausrichten auf verschiedene Arten von Benutzern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Remotedesktopdienste unterstützen unterschiedliche Typen von Arbeitsauslastungen. Skaliere deine Bereitstellung je nach den erwarteten Anforderungen jedes Benutzertyps.

## <a name="types-of-users"></a>Benutzertypen

### <a name="knowledge-user"></a>Wissensbenutzer

Wissensbenutzer verwenden einfache Produktivitätsanwendungen wie Microsoft Word, Excel, Outlook und den Microsoft Edge-Browser.

### <a name="professional-user"></a>Professionelle Benutzer

Professionelle Benutzer verwenden Internetbrowser und Produktivitätsanwendungen zusätzlich zur Unterstützung von intensiveren Arbeitsauslastungen wie der Softwareentwicklung und der Erstellung von Multimedia-Inhalten.

### <a name="power-user"></a>Poweruser

Poweruser verwenden Engineering- und Grafikanwendungen wie Programme für computergestütztes Design (CAD) und Adobe Photoshop. GPUs sind häufig eine gute Wahl für Benutzer, die regelmäßig grafikintensive Programme zum Rendern von Videos, für 3D-Entwürfe und für Simulationen verwenden.

Weitere Informationen zur Grafikbeschleunigung findest du unter [Auswählen der Grafikrenderingtechnologie](rds-graphics-virtualization.md).

Azure bietet andere Bereitstellungsoptionen für Grafikbeschleunigung sowie mehrere verfügbare GPU-VM-Größen. Weitere Informationen dazu findest du unter [Für GPU optimierte VM-Größen](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).

## <a name="test-workload"></a>Testen der Arbeitsauslastung

Es wird empfohlen, Testbereitstellungen zu laden, die sowohl Belastungstests als auch Echtzeit-Anwendungssimulationen umfassten. Auch mit Simulationstools wie LoginVSI kannst du Auslastungstest deiner Bereitstellung durchführen. Stelle sicher, dass das System reaktionsfähig und robust genug ist, um die Benutzeranforderungen zu erfüllen, und denke daran, die Ladegröße zu verändern, um böse Überraschungen zu vermeiden.
