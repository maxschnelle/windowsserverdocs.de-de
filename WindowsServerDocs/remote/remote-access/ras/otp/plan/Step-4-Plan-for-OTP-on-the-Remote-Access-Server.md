---
title: Schritt 4 Planen von OTP auf dem Remote Zugriffs Server
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 789fd72e2f3fc1693bf4803f33dcc1e7f1b3acc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855773"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>Schritt 4 Planen von OTP auf dem Remote Zugriffs Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nach der Planung der Server-und Zertifikat Einstellungen für das einmalige Kennwort (One-time password, OTP) müssen Sie den letzten Schritt bei der Planung einer Bereitstellung für den Remote Zugriff auf den RAS-Server planen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[4,1 Planen von OTP-Client Ausnahmen](#bkmk_4_1_Exemptions)|Planen Sie Ausnahmen für Benutzer ein, die für die Authentifizierung mit OTP nicht erforderlich sind.|  
|[4,2 Planen für Windows 7-Clients](#bkmk_4_2_Win7)|Planen Sie die Bereitstellung des DirectAccess-konnektivitätsassistenten (DCA) 2,0 für Windows 7-Client Computer.|  
|[4,3 Planen von Smartcards](#BKMK_smartcard)|Planen Sie die Verwendung von Smartcards für zusätzliche Autorisierung.|  
  
## <a name="41-plan-for-otp-client-exemptions"></a><a name="bkmk_4_1_Exemptions"></a>4,1 Planen von OTP-Client Ausnahmen  
Wenn die OTP-Authentifizierung aktiviert ist, müssen sich alle Benutzer standardmäßig mit einer Kombination aus Benutzername und Kennwort und OTP-Anmelde Informationen authentifizieren. Allerdings können Sie es Benutzern ermöglichen, sich nur mit einem Benutzernamen und einem Kennwort zu authentifizieren, ohne OTP zu verwenden. Erstellen Sie dazu eine Sicherheitsgruppe, und fügen Sie alle Benutzer hinzu, die von der OTP-Authentifizierung ausgenommen werden sollen.  
  
> [!NOTE]  
> Nur Client Computer aus einer einzelnen Gesamtstruktur können aufgrund der Tatsache, dass nur eine Sicherheitsgruppe für Client Ausnahmen ausgewählt werden kann, ausgenommen werden.  
  
## <a name="42-plan-for-windows-7-clients"></a><a name="bkmk_4_2_Win7"></a>4,2 Planen für Windows 7-Clients  
Windows 7-Client Computer können sich standardmäßig nicht mithilfe von OTP authentifizieren.  Windows 7-Client Computer erfordern eine DCA 2,0 für die Authentifizierung mithilfe von OTP in einer Windows Server 2012-Remote Zugriffs Bereitstellung. Weitere Informationen zu DCA 2,0 finden Sie unter [DirectAccess Connectivity Assistant 2,0](https://go.microsoft.com/fwlink/?LinkId=253699) im Microsoft Download Center.  
  
## <a name="43-plan-for-smart-cards"></a><a name="BKMK_smartcard"></a>4,3 Planen von Smartcards  
Wenn die OTP-Authentifizierung aktiviert ist, ist die Option zum Aktivieren der Verwendung von Smartcards für zusätzliche Autorisierung verfügbar. Erstellen Sie eine Sicherheitsgruppe, um vorübergehenden Zugriff zuzulassen, falls die Smartcard eines Benutzers nicht funktionsfähig ist.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Konfigurieren von DirectAccess mit OTP-Authentifizierung](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


