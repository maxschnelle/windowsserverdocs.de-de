---
title: Schritt 3 installieren und Konfigurieren von client2
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f009fdd1-94e6-4ccb-8c6e-609a5394db53
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b2d8cb1538de35a97ae83888d26abd7ad7bc8b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388319"
---
# <a name="step-3-install-and-configure-client2"></a>Schritt 3 installieren und Konfigurieren von client2

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

CLIENT2 ist ein Windows 7 @ no__t-0-Computer, der verwendet wird, um die Abwärtskompatibilität des Remote Zugriffs auf Windows Server 2016-Servern zu veranschaulichen.  
  
1. So installieren Sie das Betriebssystem auf CLIENT2 Installieren Sie Windows @ no__t-0 7 Enterprise oder Windows @ no__t-1 7 Ultimate auf client2.  
  
2. Um CLIENT2 der Corp-Domäne beizutreten. Fügen Sie CLIENT2 der Corp.contoso.com-Domäne hinzu.  
  
## <a name="to-install-the-operating-system-on-client2"></a>So installieren Sie das Betriebssystem auf CLIENT2  
  
1.  Starten Sie die Installation von Windows 7.  
  
2.  Wenn Sie zur Eingabe eines Benutzernamens aufgefordert werden, geben Sie **User1**ein. Wenn Sie zur Eingabe eines Computer namens aufgefordert werden, geben Sie **client2**ein.  
  
3.  Wenn Sie zur Eingabe eines Kennworts aufgefordert werden, geben Sie ein sicheres Kennwort zweimal ein.  
  
4.  Wenn Sie zur Eingabe der Schutzeinstellungen aufgefordert werden, klicken Sie auf **Empfohlene Einstellungen verwenden**.  
  
5.  Wenn Sie zur Eingabe des aktuellen Speicher Orts Ihres Computers aufgefordert werden, klicken Sie auf **Work Network**.  
  
6.  Verbinden Sie CLIENT2 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows 7 zu installieren, und trennen Sie die Verbindung mit dem Internet.  
  
7.  Verbinden Sie CLIENT2 mit dem Corpnet-Subnetz.  
  
## <a name="user-account-control"></a>Benutzerkontensteuerung  
Wenn Sie das Betriebssystem Windows 7 konfigurieren, müssen Sie im Dialogfeld **Benutzerkontensteuerung (User Account Control** , UAC) für einige Aufgaben auf **weiter** klicken. Einige der Konfigurationsaufgaben erfordern eine UAC-Genehmigung. Wenn Sie dazu aufgefordert werden, klicken Sie immer auf **weiter** , um diese Änderungen zu autorisieren.  
  
## <a name="to-join-client2-to-the-corp-domain"></a>So fügen Sie CLIENT2 der Corp-Domäne hinzu  
  
1.  Klicken Sie auf **Start**und mit der rechten Maustaste auf **Computer**und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie auf der Seite **System** im Bereich **Computer Name, Domäne und Arbeitsgruppen Einstellungen** auf **Einstellungen ändern**.  
  
3.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
4.  Klicken Sie im Dialogfeld **Computer Name/Domänen Änderungen** auf **Domäne**, geben Sie **Corp.contoso.com**ein, und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie den Benutzernamen und das Kennwort für das user1-Domänen Konto ein, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie, wenn das Begrüßungsdialogfeld für die Domäne %%amp;quot;corp.contoso.com%%amp;quot; angezeigt wird, auf **OK**.  
  
7.  Wenn Sie ein Dialogfeld sehen, in dem Sie aufgefordert werden, den Computer neu zu starten, klicken Sie auf **OK**.  
  
8.  Klicken Sie im Dialogfeld **System Eigenschaften** auf **Schließen**, und wenn ein Dialogfeld angezeigt wird, in dem Sie aufgefordert werden, den Computer neu zu starten, klicken Sie auf **jetzt neu starten**.  
  
9. Melden Sie sich nach dem Neustart des Computers als corp\user1 an.
