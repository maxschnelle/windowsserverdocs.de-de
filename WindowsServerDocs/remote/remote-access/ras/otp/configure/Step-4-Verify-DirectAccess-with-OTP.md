---
title: Schritt 4 Überprüfen von DirectAccess mit OTP
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83ea3c4e4feefacde3e1ed7be6b605d8c0e644a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366975"
---
# <a name="step-4-verify-directaccess-with-otp"></a>Schritt 4 Überprüfen von DirectAccess mit OTP

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen können, ob Sie DirectAccess mit OTP-Bereitstellung ordnungsgemäß konfiguriert haben.
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>So überprüfen Sie die OTP-Integrität auf dem Remote Zugriffs Server

1. Öffnen Sie auf dem Remote Zugriffs Server die **Remote Zugriffs-Verwaltungs** Konsole.  

2. Klicken Sie unter **Remote Zugriffs Server** auf den Remote Zugriffs Server, der für die OTP-Unterstützung konfiguriert wurde.  

3. Klicken Sie auf **Vorgangs Status**.  

4. Vergewissern Sie sich, dass der Status von OTP das grüne Symbol anzeigt und funktioniert.  
  
    > [!NOTE]  
    > Das Aktualisierungs Intervall für den Integritäts Status ist ein Maximum der Summe der Werte aus dem Registrierungsschlüssel hklm\system\ccs\services\ramgmtsvc\parameters\healthrefreshtimeout und dem **Zeitintervall für die Serveraktivität** , die im Remote Zugriff festgelegt wurde. konfiguri.  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>So überprüfen Sie den Zugriff auf interne Ressourcen mithilfe der OTP-Authentifizierung  
  
1.  Verbinden Sie einen DirectAccess-Client Computer mit dem Unternehmensnetzwerk, und führen Sie **gpupdate/force** an der Eingabeaufforderung aus, um die Gruppenrichtlinie zu erhalten.  
  
2.  Trennen Sie den Client Computer vom Unternehmensnetzwerk, stellen Sie eine Verbindung mit dem externen Netzwerk her, und versuchen Sie, auf interne Ressourcen zuzugreifen. Sie sollten keinen Zugriff auf die internen Ressourcen haben.  
  
3.  Im Fall eines Software Tokens greifen Sie mithilfe der Anweisungen des Anbieters auf das OTP-Client Token zu, und notieren Sie sich den aktuellen Tokencode. Wenn ein Hardware Token verwendet wird, befolgen Sie die Anweisungen des Herstellers für die Authentifizierung.  
  
4.  Klicken Sie im Infobereich auf das Symbol **Netzwerkverbindungen** , um auf die DirectAccess-Medienverwaltung zuzugreifen.  
  
5.  Klicken Sie auf die **DirectAccess-Verbindung**, und klicken Sie auf **weiter**.  
  
6.  Geben Sie den zuvor notierten Tokencode ein, und klicken Sie auf **OK**. Warten Sie, bis die Authentifizierung fertiggestellt ist. Der Status der DirectAccess-Arbeitsplatz Verbindung wird nun **verbunden**.  
  
7.  Es wurde versucht, auf interne Ressourcen zuzugreifen. Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  


