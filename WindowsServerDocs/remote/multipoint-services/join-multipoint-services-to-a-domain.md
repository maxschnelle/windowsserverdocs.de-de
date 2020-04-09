---
title: Verknüpfen von Multipoint Services mit einer Domäne (optional)
Description: Enthält die Schritte zum Verknüpfen von Multipoint Services mit Ihrer Domäne.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 03b60b1d3a7a776448eaa18d926a87a00f56fc30
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820243"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>Hinzufügen des Multipoint Services-Computers zu einer Domäne (optional)
Wenn Sie über eine Active Directory Domäne auf den Multipoint Services-Computer zugreifen werden, besteht der nächste Schritt darin, den Computer der Domäne hinzuzufügen.  
  
> [!IMPORTANT]  
> Sie müssen die Zeitzone überprüfen, bevor Sie den Computer einer Domäne hinzufügen. Anweisungen finden Sie unter [Festlegen von Datum, Uhrzeit und](Set-the-date--time--and-time-zone.md)Zeitzone.  
   
1.  Öffnen Sie auf derStartseite dieSystemsteuerung. Klicken Sie auf **System und Sicherheit**, und klicken Sie dann auf **System**.  
  
2.  Klicken Sie unter **Einstellungen für Computernamen, Domäne und Arbeitsgruppe** auf **Einstellungen ändern**.  
  
3.  Klicken Sie auf der Registerkarte **Computer Name** auf **ändern**.  
  
4.  Wählen Sie im Dialogfeld **Computer Name/Domänen Änderungen** die Option **Domäne**aus, geben Sie den Namen der Domäne ein, und klicken Sie dann auf **OK**. führen Sie dann die Schritte im Assistenten aus, um den Vorgang abzuschließen.  
  
5.  Melden Sie sich nach dem Neustart des Computers als Administrator an, und warten Sie, bis der Multipoint-Manager geöffnet wird.  
  
> [!IMPORTANT]  
> Um sicherzustellen, dass die Bereitstellung der Multipoint Services-Domäne ordnungsgemäß funktioniert, müssen Sie einige Gruppenrichtlinien konfigurieren und die Registrierung aktualisieren. Weitere Informationen finden Sie unter [Konfigurieren von Gruppenrichtlinien für eine Domänen Bereitstellung](https://technet.microsoft.com/library/dn265982.aspx).  