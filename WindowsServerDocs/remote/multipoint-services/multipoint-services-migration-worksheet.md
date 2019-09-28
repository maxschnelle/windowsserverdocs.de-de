---
title: Planen des Arbeitsblatts für die Multipoint Services-Migration
description: Stellt Planungs Arbeitsblätter bereit, um Sie bei der Migration zu Multipoint Services in Windows Server 2016 zu unterstützen.
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 864405bb-47ed-4c83-97a2-8df4c6e6f96b
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: d3d2ecca4062d28d210196d9191e08710eb731c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394626"
---
# <a name="planning-worksheet-for-multipoint-services-migration"></a>Planen des Arbeitsblatts für die Multipoint Services-Migration

>Gilt für: Windows Server 2016

Verwenden Sie die folgenden Listen und Tabellen, um die Einstellungen zu erfassen, die Sie bei der Multipoint Services-Migration benötigen.

## <a name="source-server-settings"></a>Quellservereinstellungen

Sie finden die Servereinstellungen auf der Registerkarte **Start** im Multipoint-Manager. Platzieren Sie ein Häkchen neben jeder Einstellung, die auf dem Quell Server verwendet wird.

- Gestatten Sie, dass ein Konto über mehrere Sitzungen verfügt.
- Ermöglicht die Remote Verwaltung dieses Computers.
- Hiermit wird die Überwachung der Desktops dieses Computers ermöglicht.
- Starten Sie immer im Konsolenmodus.
- Datenschutz Benachrichtigung bei der ersten Benutzeranmeldung nicht anzeigen.
- Weisen Sie jeder Station eine eindeutige IP-Adresse zu.
- Lässt zwischen dem Multipoint-Dashboard und den Benutzersitzungen auf diesem Computer zu.
- Ermöglicht die Orchestrierung von Administrator-und Multipoint-dashboardbenutzersitzungen.
- Ermöglicht Stationen die Verwendung des GPU-Hardware Rendering.

## <a name="managed-servers-and-computers"></a>Verwaltete Server und Computer

Notieren Sie die Namen der verwalteten Server und Computer. Diese Informationen finden Sie auf der Registerkarte **Startseite** im Multipoint-Manager.

| Computer | Computername |
|----------|---------------|
| 1        |               |
| 2        |               |
| 3        |               |
| 4        |               |
| 5        |               |
| 6        |               |
| 7        |               |
| 8        |               |
| 9        |               |
| 10       |               |


## <a name="stations"></a>Station

Notieren Sie die lokalen Stationen und deren Einstellungen. Diese Informationen finden Sie auf der Registerkarte **Stationen** im Multipoint-Manager.

| #  | Stationsname | Benutzerkonto für die automatische Anmeldung | Bildschirmausrichtung |
|----|--------------|-------------------------|---------------------|
| 1  |              |                         |                     |
| 2  |              |                         |                     |
| 3  |              |                         |                     |
| 4  |              |                         |                     |
| 5  |              |                         |                     |
| 6  |              |                         |                     |
| 7  |              |                         |                     |
| 8  |              |                         |                     |
| 9  |              |                         |                     |
| 10 |              |                         |                     |

## <a name="administrators-and-multipoint-dashboard-users"></a>Administratoren und Multipoint-Dashboardbenutzer

Kopieren Sie die Benutzernamen für die Benutzer von Administratoren und Multipoint-Dashboards. Diese Informationen finden Sie auf der Registerkarte **Benutzer** im Multipoint-Manager.

Administratoren:

- Benutzername:
- Benutzername:
- Benutzername:
- Benutzername:
- Benutzername:
- Benutzername:

Dashboardbenutzer:

- Benutzername:
- Benutzername:
- Benutzername:
- Benutzername:
- Benutzername:

## <a name="vdi-template-and-virtual-desktops"></a>VDI-Vorlage und virtuelle Desktops

Notieren Sie die VDI-Vorlagen Informationen und die Namen virtueller Desktops in der Multipoint Services-Bereitstellung. Diese Informationen finden Sie auf der Registerkarte **virtuelle Desktops** im Multipoint-Manager.

**Speicherort der VDI-Vorlage**: 

| # | Name des virtuellen Desktops      |
|---|---------------------------|
| 1 |                           |
| 2 |                           |
| 3 |                           |
| 4 |                           |
| 5 |                           |