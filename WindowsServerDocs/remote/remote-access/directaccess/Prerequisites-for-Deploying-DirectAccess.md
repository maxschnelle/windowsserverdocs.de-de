---
title: Erforderliche Komponenten für die Bereitstellung von DirectAccess
description: Dieses Thema enthält die Voraussetzungen für die DirectAccess-Bereitstellung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5916c5bb87d7bdb10bcc32e24647923d434de2e7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857446"
---
# <a name="prerequisites-for-deploying-directaccess"></a>Erforderliche Komponenten für die Bereitstellung von DirectAccess

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In der folgenden Tabelle sind die Voraussetzungen für die Verwendung der Konfigurations-Assistenten für die Bereitstellung von DirectAccess aufgeführt.  
  
|||  
|-|-|  
|Szenario|Erforderliche Komponenten|  
|[Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-Die Windows-Firewall muss in allen Profilen aktiviert sein.<p>-Nur für Clients unterstützt, auf denen Windows 10&reg;ausgeführt wird. <br />              Windows&reg; 8 und Windows&reg; 8,1 Enterprise.<p>-Eine Public Key-Infrastruktur ist nicht erforderlich.<p>-Wird für die Bereitstellung der zweistufigen Authentifizierung nicht unterstützt. Für die Authentifizierung sind Domänenanmeldeinformationen erforderlich.<p>-Stellt DirectAccess automatisch für alle mobilen Computer in der aktuellen Domäne bereit.<p>-Der Datenverkehr an das Internet erfolgt nicht über DirectAccess. Die Konfiguration einer Tunnelerzwingung wird nicht unterstützt.<p>-Der DirectAccess-Server ist der Netzwerkadressen Server.<p>-Netzwerk Zugriffsschutz (Network Access Protection, NAP) wird nicht unterstützt.<p>Das Ändern von Richtlinien mithilfe einer anderen Funktion als der DirectAccess-Verwaltungskonsole oder Windows PowerShell-Cmdlets wird nicht unterstützt.<p>-Verwenden Sie für eine Konfiguration mit mehreren Standorten (jetzt oder in der Zukunft) zuerst die Anleitung unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).|  
|[Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-Eine Public Key-Infrastruktur muss bereitgestellt werden.<br />    Weitere Informationen finden Sie unter [Test Umgebungs Anleitung Mini-Module: Basic PKI for Windows Server 2012](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx).<p>-Die Windows-Firewall muss in allen Profilen aktiviert sein.<p>DirectAccess wird von den folgenden Server Betriebssystemen unterstützt.<p>-Sie können alle Versionen von Windows Server 2016 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2012 R2 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2012 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<br />-Sie können alle Versionen von Windows Server 2008 R2 als DirectAccess-Client oder DirectAccess-Server bereitstellen.<p>DirectAccess wird von den folgenden Client Betriebssystemen unterstützt.<p>-Windows 10&reg; Enterprise<br />-Windows 10&reg; Enterprise 2015 Long Term Servicing Branch (ltionb)<br />-Windows&reg; 8 und 8,1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-Windows&reg; 7 Enterprise<p>-Tunnel Konfiguration erzwingen wird bei der kerbproxy-Authentifizierung nicht unterstützt.<p>Das Ändern von Richtlinien mithilfe einer anderen Funktion als der DirectAccess-Verwaltungskonsole oder Windows PowerShell-Cmdlets wird nicht unterstützt.<p>-Das Trennen von NAT64/DNS64-und IPHTTPS-Server Rollen auf einem anderen Server wird nicht unterstützt.|  
  


