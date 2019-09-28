---
title: Schritt 2 Konfigurieren des RADIUS-Servers
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00ea76d6995f875e509a3bc9ef0bab3d2689c52b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367019"
---
# <a name="step-2-configure-the-radius-server"></a>Schritt 2 Konfigurieren des RADIUS-Servers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Bevor Sie den Remote Zugriffs Server für die Unterstützung von DirectAccess mit OTP-Unterstützung konfigurieren, konfigurieren Sie den RADIUS-Server.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2,1. Konfigurieren der RADIUS-Software Verteilungs Token @ no__t-0|Konfigurieren Sie auf dem RADIUS-Server Software Verteilungs Token.|  
|[2,2. Konfigurieren der RADIUS-Sicherheitsinformationen @ no__t-0|Konfigurieren Sie auf dem RADIUS-Server die zu verwendenden Ports und den gemeinsamen geheimen Schlüssel.|  
|[2,3 Hinzufügen eines Benutzerkontos für die OTP-Überprüfung](#BKMK_Probe)|Erstellen Sie auf dem RADIUS-Server ein neues Benutzerkonto für die OTP-Überprüfung.|  
|[2,4 synchronisieren mit Active Directory](#BKMK_Active)|Erstellen Sie auf dem RADIUS-Server Benutzerkonten, die mit Active Directory Konten synchronisiert sind.|  
|[2,5 Konfigurieren des RADIUS-Authentifizierungs-Agents](#BKMK_AuthAgent)|Konfigurieren Sie den RAS-Server als RADIUS-Authentifizierungs-Agent.|  
  
## <a name="BKMK_1.1"></a>2,1 Konfigurieren der RADIUS-Software Verteilungs Token  
Der RADIUS-Server muss mit den erforderlichen Lizenz-und Software-und/oder Hardware Verteilungs Token konfiguriert werden, die von DirectAccess mit OTP verwendet werden. Dieser Prozess wird für jede Implementierung des RADIUS-Anbieters spezifisch sein.  
  
## <a name="BKMK_1.2"></a>2,2 Konfigurieren der RADIUS-Sicherheitsinformationen  
Der RADIUS-Server verwendet UDP-Ports zu Kommunikationszwecken, und jeder RADIUS-Anbieter verfügt über eigene UDP-Standardports für die eingehende und ausgehende Kommunikation. Damit der RADIUS-Server mit dem RAS-Server funktioniert, müssen Sie sicherstellen, dass alle Firewalls in der Umgebung so konfiguriert sind, dass der UDP-Datenverkehr zwischen den DirectAccess-und OTP-Servern bei Bedarf über die erforderlichen Ports zugelassen wird.  
  
Der RADIUS-Server verwendet für die Authentifizierung einen gemeinsamen geheimen Schlüssel. Konfigurieren Sie den RADIUS-Server mit einem sicheren Kennwort für den gemeinsamen geheimen Schlüssel. Beachten Sie, dass dieser verwendet wird, wenn die Client Computerkonfiguration des DirectAccess-Servers für die Verwendung mit dem OTP-Server konfiguriert wird.  
  
## <a name="BKMK_Probe"></a>2,3 Hinzufügen eines Benutzerkontos für die OTP-Überprüfung  
Erstellen Sie auf dem RADIUS-Server ein neues Benutzerkonto mit dem Namen **daprobeuser** , und geben Sie ihm das Kennwort **daprobepass**.  
  
## <a name="BKMK_Active"></a>2,4 synchronisieren mit Active Directory  
Der RADIUS-Server muss über Benutzerkonten verfügen, die den Benutzern in Active Directory entsprechen, die DirectAccess mit OTP verwenden werden.  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>So synchronisieren Sie den RADIUS-und den Active Directory Benutzer  
  
1.  Notieren Sie die Benutzerinformationen aus Active Directory für alle DirectAccess-Benutzer mit OTP-Benutzern.  
  
2.  Verwenden Sie das herstellerspezifische Verfahren, um identische Benutzer **Domänen \ Benutzernamen** Konten auf dem Server zu erstellen, die aufgezeichnet wurden.  
  
## <a name="BKMK_AuthAgent"></a>2,5 Konfigurieren des RADIUS-Authentifizierungs-Agents  
Der RAS-Server muss als RADIUS-Authentifizierungs-Agent für die Implementierung von DirectAccess mit OTP konfiguriert werden. Befolgen Sie die Anweisungen des RADIUS-Anbieters, um den RAS-Server als RADIUS-Authentifizierungs-Agent zu konfigurieren.  
  


