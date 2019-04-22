---
title: 'Schritt 4: Plan von OTP auf dem RAS-Server'
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 470eebc82177a21985afb8d0bf143427a33d65fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825441"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>Schritt 4: Plan von OTP auf dem RAS-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Der letzte Schritt bei der Planung einer Remote-Access-OTP-Bereitstellung werden nach der Planung für das Einmalkennwort (OTP) RADIUS-Server und zertifikateinstellungen, Planen von OTP-Clienteinstellungen auf dem RAS-Server.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[4.1 Planen von OTP-Client-Ausnahmen](#bkmk_4_1_Exemptions)|Planen Sie Ausnahmen für Benutzer, die nicht mit OTP-Authentifizierung erforderlich ist.|  
|[4.2 Planen Sie für Windows 7-clients](#bkmk_4_2_Win7)|Planen der DirectAccess Connectivity Assistant (DCA) 2.0 für Windows 7-Clientcomputer bereitstellen.|  
|[4.3-Plan für Smartcards](#BKMK_smartcard)|Planen Sie die Verwendung von Smartcards für zusätzliche Autorisierung.|  
  
## <a name="bkmk_4_1_Exemptions"></a>4.1 Planen von OTP-Client-Ausnahmen  
Bei der OTP-Authentifizierung aktiviert ist, wird standardmäßig alle Benutzer müssen mithilfe einer Kombination aus Benutzername und Kennwort sowie seine OTP-Anmeldeinformationen zu authentifizieren. Allerdings können Sie die ausgewählten Benutzer für die Authentifizierung mit einen Benutzernamen und das Kennwort nur ohne OTP erlauben. Zu diesem Zweck erstellen Sie eine Sicherheitsgruppe aus, und fügen Sie alle gewünschten Benutzer von OTP-Authentifizierung ausgenommen werden sollen.  
  
> [!NOTE]  
> Nur die Clientcomputer aus einer einzelnen Gesamtstruktur können aufgrund der Tatsache ausgenommen werden, nur eine Sicherheitsgruppe für Ausnahmen für Client ausgewählt werden kann.  
  
## <a name="bkmk_4_2_Win7"></a>4.2 Planen Sie für Windows 7-clients  
Standardmäßig können nicht die Windows 7-Clientcomputer mithilfe von OTP authentifizieren.  Windows 7-Clientcomputer müssen DCA 2.0 für die Authentifizierung mithilfe von OTP in einer Remote Access in Windows Server 2012-Bereitstellung. Weitere Informationen zu DCA 2.0 finden Sie unter [DirectAccess Connectivity Assistant 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) im Microsoft Download Center.  
  
## <a name="BKMK_smartcard"></a>4.3-Plan für Smartcards  
Bei der OTP-Authentifizierung aktiviert ist, ist die Option zum Aktivieren der Verwendung von Smartcards für zusätzliche Autorisierung verfügbar. Erstellen Sie eine Sicherheitsgruppe aus, um temporären Zugriff zu ermöglichen, wenn die Smartcard eines Benutzers nicht funktionsfähig ist.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Konfigurieren von DirectAccess mit OTP-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


