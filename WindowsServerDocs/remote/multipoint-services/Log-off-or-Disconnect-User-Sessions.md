---
title: Abmelden oder Trennen von Benutzersitzungen
description: Erfahren Sie, wie Sie manuell einen Benutzer abmelden
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 518e9dc9ba9603d988a7e21e08caa29db9f04bde
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854941"
---
# <a name="log-off-or-disconnect-user-sessions"></a>Abmelden oder Trennen von Benutzersitzungen
MultiPoint Services-Benutzer können anmelden und ihre Desktops Sitzungen, melden Sie sich wie bei jeder anderen Windows-Sitzung. Benutzer können auch trennen oder seine Sitzung anhalten, sodass die MultiPoint Services-Station nicht verwendet wird, aber ihre Sitzung im Arbeitsspeicher des MultiPoint Services-Systems aktiv bleibt.  
  
Darüber hinaus können Administratoren der Sitzung eines Benutzers beenden, wenn der Benutzer ihre MultiPoint Services-Sitzung verlassen oder vergessen hat, die vom System abzumelden.  
  
## <a name="logging-off-or-disconnecting-a-session"></a>Abmelden oder Trennen einer Sitzung  
In der folgenden Tabelle werden verschiedene Möglichkeiten beschrieben, mit deren Hilfe Sie bzw. andere Benutzer eine Sitzung abmelden, anhalten oder beenden können.  
  
|||  
|-|-|  
|**Aktion**|**Effect**|  
|Klicken Sie auf **starten**, klicken Sie auf Einstellungen, klicken Sie auf den Benutzernamen (in der oberen rechten Ecke), und klicken Sie dann auf **Abmelden**.|Die Sitzung wird beendet, und die Station steht für alle Benutzer zur Anmeldung zur Verfügung.|  
|Klicken Sie auf **Start**, auf **Einstellungen**, auf „Ein/Aus“ und dann auf **Trennen**.|Ihre Sitzung wird getrennt und bleibt im Arbeitsspeicher des Computers erhalten. Die Station steht für denselben sowie andere Benutzer zur Anmeldung zur Verfügung.|  
|Klicken Sie auf **starten**, klicken Sie auf Einstellungen, klicken Sie auf den Benutzernamen (in der oberen rechten Ecke), und klicken Sie dann auf **Sperren**|Die Station ist gesperrt, und Ihre Sitzung bleibt im Arbeitsspeicher des Computers erhalten.|  
  
## <a name="suspending-or-ending-a-users-session"></a>Anhalten oder Beenden einer Benutzersitzung  
In der folgenden Tabelle werden verschiedene Möglichkeiten beschrieben, mit deren Hilfe Sie als Administrator eine Benutzersitzung trennen oder beenden können.  
  
|||  
|-|-|  
|**Aktion**|**Effect**|  
|**Sperren:** Verwenden Sie im MultiPoint-Manager die **Stationen** Tab, um die benutzersitzung anzuhalten. Weitere Informationen finden Sie im Thema [Anhalten von Benutzersitzungen im aktiven Zustand](Suspend-and-Leave-User-Session-Active.md).|Die Benutzersitzung wird beendet und bleibt im Arbeitsspeicher des Computers erhalten. Die Station steht für denselben sowie andere Benutzer zur Anmeldung zur Verfügung. Der Benutzer kann sich an derselben oder einer anderen Station anmelden und seine Arbeit fortsetzen.|  
|**Ende:** Im MultiPoint-Manager verwenden die **Stationen** Registerkarte, um die Sitzung des Benutzers zu beenden. Sie können auf der Registerkarte **Stationen** auch alle Benutzersitzungen beenden. Weitere Informationen finden Sie im Thema [Beenden einer Benutzersitzung](End-a-User-Session.md).|Die Benutzersitzung wird beendet, und die Station steht für alle Benutzer zur Anmeldung zur Verfügung. Die Benutzersitzung wird nicht mehr auf der Registerkarte **Stationen** angezeigt und befindet sich auch nicht mehr im Arbeitsspeicher des Computers.|  
  
## <a name="see-also"></a>Siehe auch  
[Anhalten und Benutzersitzungen im aktiven](Suspend-and-Leave-User-Session-Active.md)  
[Beenden einer Benutzersitzung](End-a-User-Session.md)  
[Verwalten von Benutzerdesktops](manage-user-desktops-using-multipoint-dashboard.md)  
[Abmelden von Benutzersitzungen](Log-Off-User-Sessions.md)    