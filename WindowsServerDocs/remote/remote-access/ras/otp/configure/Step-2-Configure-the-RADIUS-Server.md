---
title: Schritt 2 konfigurieren den RADIUS-Server
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9c111ce52f2cca0cc37ea4d5b873c5fde12bce18
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282449"
---
# <a name="step-2-configure-the-radius-server"></a>Schritt 2 konfigurieren den RADIUS-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Vor dem Konfigurieren der RAS-Server zur Unterstützung von DirectAccess mit OTP unterstützen, konfigurieren Sie den RADIUS-Server.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2.1. Konfigurieren Sie die RADIUS-Software-Verteilung-Token](#BKMK_1.1)|Konfigurieren von Software-Verteilung-Token auf dem RADIUS-Server.|  
|[2.2. Konfigurieren Sie die Sicherheitsinformationen für RADIUS](#BKMK_1.2)|Konfigurieren Sie die Ports und den gemeinsamen geheimen Schlüssel verwendet werden, auf dem RADIUS-Server.|  
|[2.3 hinzufügen-Benutzerkonto für die OTP-Tests](#BKMK_Probe)|Erstellen Sie ein neues Benutzerkonto für die OTP-Tests, auf dem RADIUS-Server.|  
|[2.4 synchronisieren Sie mit Active Directory.](#BKMK_Active)|Erstellen Sie Benutzerkonten, die mit Active Directory-Konten synchronisiert, auf dem RADIUS-Server.|  
|[2.5 Konfigurieren des RADIUS-Authentifizierungs-Agents](#BKMK_AuthAgent)|Konfigurieren der RAS-Server als RADIUS-Authentifizierung-Agent.|  
  
## <a name="BKMK_1.1"></a>2.1 Konfigurieren Sie, die RADIUS-Software-Verteilung-Token  
Der RADIUS-Server muss konfiguriert werden, mit dem erforderliche Lizenz und Software und/oder-Hardware Verteilung-Token, die von DirectAccess mit OTP verwendet werden. Dieser Prozess wird für jeden RADIUS-herstellerimplementierung spezifisch sein.  
  
## <a name="BKMK_1.2"></a>2.2 Konfigurieren Sie die Sicherheitsinformationen für die RADIUS-  
Der RADIUS-Server verwendet die UDP-Ports für die Kommunikation verwendet, und jeder RADIUS-Anbieter hat einen eigenen Standard-UDP-Ports für die eingehende und ausgehende Kommunikation. Für den RADIUS-Server zum Arbeiten mit dem RAS-Server sicher, dass alle Firewalls in der Umgebung für die UDP-Datenverkehr zwischen dem DirectAccess und OTP-Server über die erforderlichen Ports zulassen, je nach Bedarf konfiguriert werden.  
  
Der RADIUS-Server verwendet einen gemeinsamen geheimen Schlüssel zum Zweck der Authentifizierung. Konfigurieren des RADIUS-Servers durch ein sicheres Kennwort für den gemeinsamen geheimen Schlüssel ein, und beachten Sie, dass dies verwendet wird, wenn der DirectAccess-Server Client Computer-Konfiguration für die Verwendung mit DirectAccess mit OTP zu konfigurieren.  
  
## <a name="BKMK_Probe"></a>2.3 hinzufügen-Benutzerkonto für die OTP-Tests  
Erstellen Sie auf dem RADIUS-Server ein neues Benutzerkonto namens **DAProbeUser** und weisen Sie ihm das Kennwort **"daprobepass"** .  
  
## <a name="BKMK_Active"></a>2.4 synchronisieren Sie mit Active Directory.  
Der RADIUS-Server muss Benutzerkonten verfügen, die die Benutzer in Active Directory zu entsprechen, die DirectAccess mit OTP verwenden möchten.  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>Um die RADIUS- und Active Directory-Benutzer zu synchronisieren.  
  
1.  Notieren Sie die Benutzerinformationen aus Active Directory für alle DirectAccess mit OTP-Benutzern.  
  
2.  Gehen Sie Anbieter bestimmte zum Erstellen identischen Benutzers **"Domäne\Benutzername"** -Konten in der RADIUS-Server, die aufgezeichnet wurden.  
  
## <a name="BKMK_AuthAgent"></a>2.5 Konfigurieren des RADIUS-Authentifizierungs-Agents  
RAS-Server muss als ein RADIUS-Authentifizierungs-Agent für DirectAccess mit OTP-Implementierung konfiguriert werden. Führen Sie die Anweisungen für die RADIUS-Anbieters, um die RAS-Servers als RADIUS-Authentifizierung-Agent zu konfigurieren.  
  


