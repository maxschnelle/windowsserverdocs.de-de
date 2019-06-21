---
title: Erforderliche Komponenten für die Bereitstellung von DirectAccess
description: Dieses Thema enthält die Voraussetzungen für die Bereitstellung von DirectAccess in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f77df438ba2b282101a031b4ff4d145286cf3e94
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283624"
---
# <a name="prerequisites-for-deploying-directaccess"></a>Erforderliche Komponenten für die Bereitstellung von DirectAccess

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgende Tabelle enthält die notwendigen Voraussetzungen für die Verwendung von der Konfigurations-Assistenten zum Bereitstellen von DirectAccess.  
  
|||  
|-|-|  
|Szenario|Vorraussetzungen|  
|[Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-Windows Firewall muss in allen Profilen aktiviert sein<br /><br />– Nur für Clients unter Windows 10 unterstützt&reg;, <br />              Windows&reg; 8 und Windows&reg; 8.1 Enterprise.<br /><br />– Eine public Key-Infrastruktur ist nicht erforderlich.<br /><br />-Nicht für die Bereitstellung von zwei-Faktor-Authentifizierung unterstützt. Für die Authentifizierung sind Domänenanmeldeinformationen erforderlich.<br /><br />-Wird Sie DirectAccess automatisch auf allen mobilen Computern in der aktuellen Domäne bereitgestellt.<br /><br />-Datenverkehr an das Internet wird über DirectAccess nicht übertragen. Die Konfiguration einer Tunnelerzwingung wird nicht unterstützt.<br /><br />-DirectAccess Server ist der Netzwerkadressenserver.<br /><br />-Network Access Protection (NAP) wird nicht unterstützt.<br /><br />– Ändern von Richtlinien mit einer Funktion als der DirectAccess-Verwaltungskonsole oder der Windows PowerShell-Cmdlets wird nicht unterstützt.<br /><br />-Bei einer Konfiguration mit mehreren Standorten, jetzt oder in der Zukunft und führen Sie zunächst die Anleitungen im [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).|  
|[Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|– Eine public Key-Infrastruktur muss bereitgestellt werden.<br />    Weitere Informationen finden Sie unter [Test Testumgebungsanleitung – Minimodul: Einfache PKI für WindowsServer 2012](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx).<br /><br />-Windows-Firewall muss in allen Profilen aktiviert sein.<br /><br />Die folgenden Serverbetriebssysteme wird DirectAccess unterstützt.<br /><br />– Sie können alle Versionen von Windows Server 2016 als einem DirectAccess-Client oder einem DirectAccess-Server bereitstellen.<br />– Sie können alle Versionen von Windows Server 2012 R2 als ein DirectAccess-Client oder einem DirectAccess-Server bereitstellen.<br />– Sie können alle Versionen von Windows Server 2012 als ein DirectAccess-Client oder einem DirectAccess-Server bereitstellen.<br />– Sie können alle Versionen von Windows Server 2008 R2 als ein DirectAccess-Client oder einem DirectAccess-Server bereitstellen.<br /><br />Die folgenden Client-Betriebssysteme wird DirectAccess unterstützt.<br /><br />-Windows 10&reg; Enterprise<br />-Windows 10&reg; Enterprise-2015, Long-Term Servicing Branch (LTSB)<br />-Windows&reg; 8 und 8.1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-Windows&reg; 7 Enterprise<br /><br />-Die Konfiguration einer tunnelerzwingung wird mit KerbProxy Authentifizierung nicht unterstützt.<br /><br />– Ändern von Richtlinien mit einer Funktion als der DirectAccess-Verwaltungskonsole oder der Windows PowerShell-Cmdlets wird nicht unterstützt.<br /><br />-Trennen von NAT64/DNS64 und IPHTTPS-Serverrollen auf einem anderen Server wird nicht unterstützt.|  
  


