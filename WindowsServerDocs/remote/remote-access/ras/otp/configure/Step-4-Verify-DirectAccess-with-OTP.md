---
title: Schritt 4 Überprüfen von DirectAccess mit OTP
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
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bcc152723ee339c8652c9480647bfb8f438c87d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813241"
---
# <a name="step-4-verify-directaccess-with-otp"></a>Schritt 4 Überprüfen von DirectAccess mit OTP

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt, wie Sie sicher, dass Sie ordnungsgemäß von DirectAccess mit OTP-Bereitstellung konfiguriert haben.
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>So überprüfen OTP-Integrität auf dem RAS-server

1. Klicken Sie auf dem Remotezugriffsserver die **Remotezugriffsverwaltung** Konsole.  

2. Klicken Sie unter **RAS-Server** klicken Sie auf dem RAS-Server, die Unterstützung von OTP konfiguriert wurde.  

3. Klicken Sie auf **Vorgangsstatus**.  

4. Stellen Sie sicher, dass der Status des OTP das grüne Symbol zeigt und funktionstüchtig ist.  
  
    > [!NOTE]  
    > Das Intervall zum Aktualisieren des Status von Integrität werden maximal die Summe der Werte aus dem Registrierungsschlüssel HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout und **Zeitintervall für die Serveraktivität** , festgelegt wurde, der DirectAccess-Konfiguration.  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>Um den Zugriff auf interne Ressourcen, die mithilfe der OTP-Authentifizierung überprüfen  
  
1.  Einen DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk herstellen, und führen Sie **Gpupdate/force** an der Eingabeaufforderung aus, um die Gruppenrichtlinie zu erhalten.  
  
2.  Trennen Sie den Clientcomputer aus dem Unternehmensnetzwerk, eine Verbindung mit dem externen Netzwerk herstellen Sie und auf interne Ressourcen zuzugreifen versuchen. Sie sollten nicht auf die internen Ressourcen zugreifen.  
  
3.  Klicken Sie im Fall von einem Softwaretoken wird Zugriff auf die OTP-Client-Token mit den Anweisungen des Anbieters, und notieren Sie den Code des aktuellen token. Wenn ein Hardwaretoken verwendet wird, befolgen Sie die Anweisungen des Anbieters für die Authentifizierung.  
  
4.  Klicken Sie im Infobereich auf das Symbol **Netzwerkverbindungen** , um auf die DirectAccess-Medienverwaltung zuzugreifen.  
  
5.  Klicken Sie auf die **DirectAccess-Verbindung**, und klicken Sie auf **Weiter**.  
  
6.  Geben Sie den token Code, der sich zuvor notiert haben, und klicken Sie auf **OK**. Warten Sie, für die Authentifizierung abzuschließen. Der DirectAccess-Arbeitsplatz-Verbindungsstatus werden **verbunden**.  
  
7.  Es wurde versucht auf interne Ressourcen zugreifen. Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  


