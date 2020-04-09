---
title: Anpassen der Aufgabe "Anmelden bei Microsoft Online Backup Service"
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3318ca3937cdc054889121a830bc3eafec4d6acf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818083"
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Anpassen der Aufgabe "Anmelden bei Microsoft Online Backup Service"

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Standardmäßig wird über die Aufgabe **Für Microsoft Online Backup Service anmelden** auf der Registerkarte **GERÄTE** des Dashboards die Microsoft Online Backup Service-Website geöffnet. Die Website stellt Informationen zum Dienst bereit und hilft Ihnen, den Dienst zu abonnieren und die erforderliche Software herunterzuladen.  
  
 Ihnen stehen zwei Möglichkeiten zur Verfügung, um die Aufgabe **Bei Microsoft Online Backup Service anmelden** anzupassen:  
  
-   Sie können die URL für die Standardwebsite durch eine URL mit angepasster Benutzerfreundlichkeit ersetzen. Um die Standard-URL zu ersetzen, öffnen Sie den Registrierungs-Editor und erstellen den Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl**. Weisen Sie dann die benutzerdefinierte URL als Wert für den Schlüssel zu.  
  
-   Sie können die Aufgabe ausblenden. Um die Aufgabe auszublenden, öffnen Sie den Registrierungs-Editor und erstellen den folgenden Registrierungsschlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled**.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)