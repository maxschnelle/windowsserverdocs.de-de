---
title: Verknüpfen von MultiPoint Services zu einer Domäne (optional)
Description: Enthält die Schritte zum MultiPoint Server Ihrer Domäne beitreten
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: af5dd1f16e011161bbcf72c21c21088721ac1243
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827041"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>Fügen Sie den MultiPoint Services-Computer einer Domäne (optional)
Wenn Sie auf dem MultiPoint Services-Computer über Active Directory-Domäne zugreifen, ist der nächste Schritt, den Computer der Domäne hinzufügen.  
  
> [!IMPORTANT]  
> Sie müssen Ihre Zeitzone überprüfen, bevor der Computer einer Domäne beitreten. Anweisungen hierzu finden Sie unter [legen Sie das Datum, Uhrzeit und Zeitzone](Set-the-date--time--and-time-zone.md).  
   
1.  Öffnen Sie auf der **Startseite die ****Systemsteuerung**. Klicken Sie auf **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe**auf **Einstellungen ändern**.  
  
3.  Auf der **Computername** auf **Änderung**.  
  
4.  In der **Änderung des Computernamens bzw. der Domäne** wählen Sie im Dialogfeld **Domäne**, geben Sie den Namen der Domäne, und klicken Sie auf **OK**, und klicken Sie dann die Schritte im Assistenten zum Abschließen der der Prozess.  
  
5.  Nach dem Neustart des Computers melden Sie sich als Administrator, und Warten von MultiPoint-Manager zu öffnen.  
  
> [!IMPORTANT]  
> Um sicherzustellen, dass Ihr MultiPoint Services-Domäne-Bereitstellung ordnungsgemäß funktioniert, müssen Sie eine Reihe von Gruppenrichtlinien zu konfigurieren und aktualisieren Sie die Registrierung. Weitere Informationen finden Sie unter [Konfigurieren von Gruppenrichtlinien für eine domänenbereitstellung](https://technet.microsoft.com/library/dn265982.aspx).  