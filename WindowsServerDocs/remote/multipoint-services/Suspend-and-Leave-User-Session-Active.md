---
title: Anhalten von Benutzersitzungen im aktiven Zustand
description: Erfahren Sie, wie Sie einen Benutzer aus einer Multipoint-Sitzung aussetzen, ohne die Verbindung zu trennen.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 0ef9d98584df568438cc3c905a7c86cd58f53343
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394925"
---
# <a name="suspend-and-leave-user-session-active"></a>Anhalten von Benutzersitzungen im aktiven Zustand
Wenn Sie die Sitzungen der Benutzer nicht beenden möchten, können Sie die Verbindung zwischen Benutzern und dem Multipoint Services-System trennen oder aussetzen. Ein Benutzer kann eine Sitzung auch selbst trennen. Während eine Benutzersitzung angehalten wird, bleibt die Sitzung im Arbeitsspeicher des Multipoint Services-Systems aktiv, bis der Computer heruntergefahren oder neu gestartet wird. Zu diesem Zeitpunkt werden alle angehaltenen Sitzungen beendet, und sämtliche nicht gespeicherte Arbeit geht verloren.  
  
1.  Öffnen Sie den Multipoint-Manager im Stations Modus, und klicken Sie dann auf die Registerkarte **Stationen** .  
  
2.  Klicken Sie in der Spalte **Computer** auf den Namen des Computers, dessen Sitzungen Sie anhalten möchten.  
  
3.  Klicken Sie unter **Stationsaufgaben** auf **Alle Stationen anhalten**.  
  
Nachdem eine Benutzersitzung angehalten wurde, kann sich der Benutzer an derselben oder einer anderen Station anmelden und seine Arbeit in der ursprünglichen Sitzung fortsetzen.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Benutzer Desktops](manage-user-desktops-using-multipoint-dashboard.md)  
[Abmelden oder Trennen von Benutzersitzungen](Log-off-or-Disconnect-User-Sessions.md)