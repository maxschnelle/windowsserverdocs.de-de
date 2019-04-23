---
title: Konfigurieren von Host-Überwachungsdienst für Https-Kommunikation
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 83529a5bdb4547b9881bb307a8a4cd526552d02c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829001"
---
# <a name="configure-hgs-for-https-communications"></a>Konfigurieren von Host-Überwachungsdienst für HTTPS-Kommunikation

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In der Standardeinstellung beim Initialisieren des HGS-Servers wird die IIS-Websites für die nur für HTTP-Kommunikation konfiguriert.
Alle vertraulichen Materials zum und vom Host-Überwachungsdienst übertragenen sind always encrypted mithilfe von Verschlüsselung auf Nachrichtenebene, aber wenn Sie eine höhere Sicherheitsstufe wünschen Sie auch HTTPS aktivieren können durch Konfigurieren von Host-Überwachungsdienst mit einem SSL-Zertifikat.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

