---
title: "Anpassen der anmelden für Microsoft Online Backup Service-Vorgang"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cd148e0e58cd80dbff7f7884ead95dc1e46b6257
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Anpassen der anmelden für Microsoft Online Backup Service-Vorgang

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Standardmäßig die **für Microsoft Online Backup Service anmelden** Aufgabe auf den **Geräte** Dashboard-Registerkarte geöffnet wird, die Microsoft Online Backup Service-Website. Die Website bietet Informationen über den Dienst, und hilft Ihnen, den Dienst abonnieren und die erforderliche Software herunterzuladen.  
  
 Sie können anpassen, die **für Microsoft Online Backup Service anmelden** Aufgabe auf zwei Arten:  
  
-   Sie können die URL für die Standardwebsite durch eine URL ersetzen, die eine benutzerdefinierte Benutzeroberfläche darstellt. Um die Standard-URL zu ersetzen, Registrierungs-Editor zu öffnen, erstellen Sie den Registrierungsschlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl**, und weisen Sie die benutzerdefinierte URL als Wert für den Schlüssel.  
  
-   Sie können die Aufgabe ausblenden. Um die Aufgabe auszublenden, Registrierungs-Editor zu öffnen, und erstellen den Registrierungsschlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled **.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)