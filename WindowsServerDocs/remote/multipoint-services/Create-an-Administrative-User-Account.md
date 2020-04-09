---
title: Erstellen eines Administratorkontos
description: Erstellen eines Kontos mit Administratorrechten in Multipoint Services
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 8ce4c5a9-3dec-412f-910b-54a252f8f209
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 72b7517d35d18064806d3df35f2f9ed7b636df8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859773"
---
# <a name="create-an-administrative-user-account"></a>Erstellen eines Administratorkontos
Erstellen Sie *Administratorkonten* für diejenigen Benutzer, die das MultiPoint Services-System verwalten werden. Um zu ermitteln, wer über Administrator Zugriff verfügt, klicken Sie in Multipoint-Manager auf die Registerkarte **Benutzer** . administrative Benutzerkonten werden in der Spalte **Kontotyp** als **Administrator**angezeigt. Administratoren *haben Zugriff* auf alle Multipoint Manager-Aufgaben, die Desktop-und Systemeinstellungen ändern, wie z. b.:  
  
-   Erstellen von Konten  
  
-   Hinzufügen und Entfernen von Programmen  
  
-   Verwalten von *Desktops* und Hardware  
  
-   Beenden von *Sitzungen* anderer Benutzer  
  
Administratoren können Aufgaben ausführen, die sich auf alle anderen Benutzer des MultiPoint Services-Systems auswirken, wie z.B. die Installation von Software oder die Änderung von Sicherheitseinstellungen. Aus diesem Grund sollten Administratoren über eindeutige Benutzernamen und Kennwörter verfügen, die nur ihnen bekannt sind.  
  
Weitere Informationen zu Problemen, die Sie als Administrator beim Erstellen und Verwalten von Benutzerkonten berücksichtigen sollten, finden Sie im Thema [Überlegungen zu Benutzerkonten](User-Account-Considerations.md).  
  
> [!NOTE]  
> Sie können auch für sich selbst ein *Standardbenutzerkonto* erstellen, das Sie zur Ausführung von Aufgaben im MultiPoint Services-System verwenden können, die nicht mit der Verwaltung des MultiPoint Services-Systems in Zusammenhang stehen. In diesem Fall melden Sie sich nur dann bei Ihrem Administratorkonto an, wenn Systemverwaltungsaufgaben auszuführen sind.  
  
#### <a name="to-create-an-administrative-user-account"></a>So erstellen Sie ein Administratorkonto  
  
1.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Benutzer** .  
  
2.  Klicken Sie unter **Benutzeraufgaben** auf **Benutzerkonto hinzufügen**. Der Assistent **Benutzerkonto hinzufügen** wird geöffnet.  
  
3.  Geben Sie in das Feld **Benutzerkonto** einen Anmeldenamen für den Benutzer ein. Typischerweise besteht der Anmeldename des Benutzers aus dem Vor- und Nachnamen, die ohne Leerzeichen in einem Wort zusammengeschrieben werden, oder dem ersten Buchstaben des Vornamens und dem Nachnamen, die ohne Leerzeichen in einem Wort zusammengeschrieben werden.  
  
4.  Geben Sie in das Feld **Vollständiger Name** den Namen des Benutzers im gewünschten Format ein, z.B. Vorname, vollständiger Name oder Spitzname.  
  
5.  Geben Sie im Feld **Kennwort** ein Kennwort für den Benutzer ein. Dieses Kennwort sollte nur Ihnen und dem Benutzer bekannt sein und muss an einem sicheren Ort gespeichert werden. Das Kennwort kann nur von einem Administrator geändert werden.  
  
6.  Geben Sie das Kennwort im Feld **Kennwort bestätigen** erneut ein, und klicken Sie dann auf **Weiter**.  
  
7.  Wählen Sie auf der Seite zum Festlegen der Zugriffsebene die Option **Administrator** aus, und klicken Sie dann auf **Weiter**.  
  
8.  MultiPoint Services überprüft alle Informationen und zeigt im Anschluss an die Einrichtung des Kontos eine Meldung an. Wenn der Text **Ein neues Benutzerkonto wurde erfolgreich erstellt** angezeigt wird, klicken Sie auf **Fertig stellen**.  
