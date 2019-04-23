---
title: Konfigurieren von Gruppenrichtlinien für eine Domänenbereitstellung
description: Erfahren Sie, wie Sie Gruppenrichtlinien in MultiPoint Services einrichten
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: f661fbdc40fd7dd2562d51756bc7642c8e9a4a82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888041"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>Konfigurieren von Gruppenrichtlinien für eine Domänenbereitstellung
Um sicherzustellen, dass Ihre Bereitstellung von MultiPoint Services ordnungsgemäß funktioniert, wenden Sie die folgenden gruppenrichtlinieneinstellungen zum WMSshell Benutzerkonto in einem MultiPoint Services-System.  
  
> [!IMPORTANT]  
> Einige der gruppenrichtlinieneinstellungen können verhindern, dass die erforderlichen Konfigurationseinstellungen mit MultiPoint Services angewendet werden. Achten Sie darauf, dass Sie verstehen, und Ihr gruppenrichtlinieneinstellungen zu definieren, damit sie ordnungsgemäß in MultiPoint Services funktionieren. Beispielsweise könnte eine gruppenrichtlinieneinstellung, die automatische Anmeldung wird verhindert, dass Probleme mit MultiPoint Services-Anmeldung Verhalten darstellen.  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>Aktualisieren von Gruppenrichtlinien für das Benutzerkonto WMSshell 
Das Benutzerkonto WMSshell ist ein Systemkonto, der MultiPoint Services wird verwendet, um Sign-in die Konsole, in die Stationen Actuall erstellt werden. Dieses Konto ist nicht mentar von MultiPoint-Manager verwaltet werden.
  
> [!NOTE]  
> Um herauszufinden, wie Gruppenrichtlinien aktualisieren, finden Sie unter [Editor für lokale Gruppenrichtlinien](https://technet.microsoft.com/library/dn265982.aspx).  
  
**RICHTLINIE:** Benutzerkonfiguration > Administrative Vorlagen > Systemsteuerung > **Personalisierung**  
  
Weisen Sie die folgenden Werte ein:  
  
|Einstellung|Werte|  
|-----------|----------|  
|Bildschirmschoner aktiv|Deaktiviert|  
|Zeitlimit für Bildschirmschoner|Deaktiviert<br /><br />Sekunden: Xxx|  
|Kennwortschutz für den Bildschirmschoner verwenden|Deaktiviert|  
  
**RICHTLINIE:** Computerkonfiguration > Windows-Einstellungen > Sicherheitseinstellungen > Lokale Richtlinien > Zuweisen von Benutzerrechten > **lokal anmelden zulassen**  
  
|Einstellung|Werte|  
|-----------|----------|  
|Lokale Anmeldung zulassen|Stellen Sie sicher, dass die Liste der Konten das WMSshell-Konto enthält.<br /><br />**Hinweis**: Standardmäßig ist das WMSshell-Konto ein Mitglied der Benutzergruppe. Wenn die Gruppe Benutzer in der Liste ist und WMSshell ein Mitglied der Benutzergruppe ist, müssen Sie nicht das WMSshell-Konto zur Liste hinzuzufügen.|  
  
> [!IMPORTANT]  
> Wenn Sie keine Gruppenrichtlinien festlegen, stellen Sie sicher, dass die Richtlinien nicht automatische Updates "und" Fehler beim Windows-Fehlerberichterstattung auf dem MultiPoint Server beeinträchtigen. Diese werden festgelegt, indem die **updates automatisch installieren** und **automatische Windows-Fehlerberichterstattung** Einstellungen, die während der Installation Windows MultiPoint Server in MultiPoint konfiguriert ausgewählt wurden Manager mithilfe von **Bearbeiten von servereinstellungen**, oder bei der geplanten Aktualisierung für den Datenträger-Schutz konfiguriert.  
  
## <a name="update-the-registry"></a>Aktualisieren Sie die Registrierung  
Für eine domänenbereitstellung MultiPoint Services sollten Sie die folgenden Registrierungsunterschlüssel aktualisieren.  
  
> [!IMPORTANT]  
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>Aktualisieren von Registrierungsunterschlüsseln für eine domänenbereitstellung MultiPoint Services  
  
1.  Registrierungs-Editor zu öffnen. (Geben Sie an einer Eingabeaufforderung den Befehl **regedit.exe**, und drücken Sie EINGABETASTE.)  
  
2.  Klicken Sie im linken Bereich Suchen Sie, und wählen Sie dann den folgenden Registrierungsunterschlüssel:  
  
    HKEY_USERS\<SIDofWMSshell>\Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    wobei "<SIDofWMSshell>" wird die Sicherheits-ID (SID) für das Konto WMSshell. Um herauszufinden, wie die SID zu identifizieren, finden Sie unter [einen Benutzernamen mit einer Sicherheits-ID (SID) zuordnen](https://support.microsoft.com/kb/154599).  
  
3.  Aktualisieren Sie die folgenden Unterschlüssel in der Liste auf der rechten Seite.  
  
    |Unterschlüssel|Wertname|Wertdaten|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (null)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (null)|  
  
    So aktualisieren Sie einen Registrierungsunterschlüssel:  
  
    1.  Der Registrierungsschlüssel, der im linken Bereich ausgewählt wird, mit der rechten Maustaste des Unterschlüssels im rechten Bereich, und klicken Sie dann auf **ändern**.  
  
    2.  Geben Sie im Dialogfeld Zeichenfolge bearbeiten, einen neuen Wert in **Wertdaten**, und klicken Sie dann auf **OK**.  
  
4.  Nach Abschluss der Aktualisierung von Registrierungsunterschlüsseln für starten Sie den Computer zur Aktivierung der Änderungen neu. 