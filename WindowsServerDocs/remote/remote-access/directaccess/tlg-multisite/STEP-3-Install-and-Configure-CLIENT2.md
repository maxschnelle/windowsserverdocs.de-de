---
title: Schritt 3 installieren und Konfigurieren von CLIENT2
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f009fdd1-94e6-4ccb-8c6e-609a5394db53
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2c7ff4953fd4369340f55f40f93cfc01d4240b26
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281459"
---
# <a name="step-3-install-and-configure-client2"></a>Schritt 3 installieren und Konfigurieren von CLIENT2

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

CLIENT2 ist ein Windows 7&reg; Computer, der verwendet wird, um zu veranschaulichen die Abwärtskompatibilität Kompatibilität des Remotezugriffs auf Windows Server 2016-Servern ausgeführt werden.  
  
1. Zum Installieren des Betriebssystems auf CLIENT2. Installieren Sie Windows&reg; 7 Enterprise oder Windows&reg; 7 Ultimate auf CLIENT2.  
  
2. CLIENT2 mit der CORP-Domäne zu verknüpfen. Fügen Sie der Domäne "corp.contoso.com" CLIENT2.  
  
## <a name="to-install-the-operating-system-on-client2"></a>So installieren Sie das Betriebssystem auf CLIENT2  
  
1.  Starten Sie die Installation von Windows 7.  
  
2.  Wenn Sie für einen Benutzernamen aufgefordert werden, geben Sie **"user1"** . Wenn Sie für eines Computernamens aufgefordert werden, geben Sie **CLIENT2**.  
  
3.  Wenn Sie nach einem Kennwort gefragt werden, ein sicheres Kennwort zweimal eingeben.  
  
4.  Wenn Sie für Protection-Einstellungen aufgefordert werden, klicken Sie auf **empfohlene Einstellungen verwenden**.  
  
5.  Wenn Sie für den aktuellen Standort des Computers aufgefordert werden, klicken Sie auf **Firmennetzwerk**.  
  
6.  Verbinden von CLIENT2 mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows 7 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
7.  Verbinden Sie CLIENT2, mit dem Subnetz "Corpnet".  
  
## <a name="user-account-control"></a>Benutzerkontensteuerung  
Wenn Sie das Betriebssystem Windows 7 konfigurieren, müssen Sie auf **Weiter** auf die **User Account Control** (UAC) Dialogfeld für einige Aufgaben. Einige der Konfigurationsaufgaben müssen UAC genehmigt werden. Wenn Sie aufgefordert werden, klicken Sie immer auf **Weiter** um diese Änderungen zu autorisieren.  
  
## <a name="to-join-client2-to-the-corp-domain"></a>CLIENT2 mit der CORP-Domäne zu verknüpfen  
  
1.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**.  
  
2.  Auf der **System** auf der Seite die **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** Bereich, klicken Sie auf **Ändern der Einstellungen**.  
  
3.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
4.  Auf der **Änderung des Computernamens bzw. der Domäne** Dialogfeld klicken Sie auf **Domäne**, Typ **"corp.contoso.com"** , und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für das Domänenkonto "user1", und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie, wenn das Begrüßungsdialogfeld für die Domäne %%amp;quot;corp.contoso.com%%amp;quot; angezeigt wird, auf **OK**.  
  
7.  Wenn ein Dialogfeld angezeigt wird, aufgefordert, den Computer neu starten, klicken Sie auf **OK**.  
  
8.  Auf der **Systemeigenschaften** Dialogfeld klicken Sie auf **schließen**, und wenn Sie ein Dialogfeld, das aufgefordert, den Computer neu starten, klicken Sie auf **jetzt neu starten**.  
  
9. Melden Sie sich nach dem Neustart des Computers als "corp\user1" an.
