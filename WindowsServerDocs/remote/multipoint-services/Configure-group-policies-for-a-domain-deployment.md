---
title: Konfigurieren von Gruppenrichtlinien für eine Domänenbereitstellung
description: Erfahren Sie, wie Sie Gruppenrichtlinien in Multipoint Services einrichten.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 9c01bdd45b5aa88a8ce4f8a5876a0f3cbc3c0cc3
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966312"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>Konfigurieren von Gruppenrichtlinien für eine Domänenbereitstellung
Um sicherzustellen, dass Ihre Domänen Bereitstellung von Multipoint Services ordnungsgemäß funktioniert, wenden Sie die folgenden Gruppenrichtlinien Einstellungen auf das wmsshell-Benutzerkonto in einem Multipoint Services-System an.  
  
> [!IMPORTANT]  
> Einige Gruppenrichtlinien Einstellungen können verhindern, dass erforderliche Konfigurationseinstellungen auf Multipoint Services angewendet werden. Stellen Sie sicher, dass Sie Ihre Gruppenrichtlinien Einstellungen verstehen und definieren, damit Sie in Multipoint Services ordnungsgemäß funktionieren. Beispielsweise kann eine Gruppenrichtlinie Einstellung, die die automatische Anmeldung verhindert, Probleme mit dem Multipoint Services-Anmeldeverhalten darstellen.  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>Aktualisieren von Gruppenrichtlinien für das wmsshell-Benutzerkonto 
Beim wmsshell-Benutzerkonto handelt es sich um ein Systemkonto, das von Multipoint Services zum Anmelden in der-Konsole verwendet wird, in der die eigentlichen Stationen erstellt werden. Dieses Konto soll nicht von Multipoint Manager verwaltet werden.
  
> [!NOTE]  
> Informationen zum Aktualisieren von Gruppenrichtlinien finden Sie unter [Editor für lokale Gruppenrichtlinien](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265982(v=ws.11)).  
  
**Richtlinie:** Benutzerkonfiguration > administrative Vorlagen > Systemsteuerung > **Personalisierung**  
  
Weisen Sie die folgenden Werte zu:  
  
|Einstellung|Werte|  
|-----------|----------|  
|Bildschirmschoner aktivieren|Disabled|  
|Zeitlimit für Bildschirmschoner|Disabled<p>Sekunden: xxx|  
|Kennwortschutz für den Bildschirmschoner verwenden|Disabled|  
  
**Richtlinie:** Computer Konfiguration >Windows-Einstellungen >Sicherheitseinstellungen >lokale Richtlinien >Zuweisen von Benutzerrechten > **Lokal anmelden zulassen**  
  
|Einstellung|Werte|  
|-----------|----------|  
|Lokale Anmeldung zulassen|Stellen Sie sicher, dass die Liste der Konten das wmsshell-Konto enthält.<p>**Hinweis:** Standardmäßig ist das wmsshell-Konto Mitglied der Gruppe "Benutzer". Wenn die Gruppe "Benutzer" in der Liste enthalten ist und wmsshell Mitglied der Gruppe "Benutzer" ist, müssen Sie das wmsshell-Konto nicht zur Liste hinzufügen.|  
  
> [!IMPORTANT]  
> Wenn Sie Gruppenrichtlinien festlegen, stellen Sie sicher, dass die Richtlinien die automatischen Updates und die Fehlerberichterstattung für Fehlerberichte auf dem Multipoint-Server nicht beeinträchtigen. Diese werden von den Einstellungen **Updates automatisch installieren** und automatisch **Windows-Fehlerberichterstattung** festgelegt, die bei der Installation von Windows MultiPoint Server ausgewählt, in Multipoint Manager mithilfe von **Server Einstellungen bearbeiten**oder in geplanten Updates für den Datenträger Schutz konfiguriert wurden.  
  
## <a name="update-the-registry"></a>Aktualisieren der Registrierung  
Für eine Domänen Bereitstellung von Multipoint Services sollten Sie die folgenden Registrierungs Unterschlüssel aktualisieren.  
  
> [!IMPORTANT]  
> Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>So aktualisieren Sie Registrierungs Unterschlüssel für eine Domänen Bereitstellung von Multipoint Services  
  
1.  Öffnen Sie den Registrierungs-Editor. (Geben Sie an einer Eingabeaufforderung **regedit.exe**ein, und drücken Sie die EINGABETASTE.)  
  
2.  Suchen Sie im linken Bereich den folgenden Registrierungs Unterschlüssel, und wählen Sie ihn aus:  
  
    HKEY_USERS \<SIDofWMSshell> \software\policies\microsoft\windows\systemsteuerung\desktop  
  
    dabei <SIDofWMSshell> ist "" die Sicherheits-ID (SID) für das wmsshell-Konto. Informationen dazu, wie Sie die SID identifizieren, finden Sie unter [Zuordnen eines Benutzernamens zu einer Sicherheits-ID (SID)](https://support.microsoft.com/kb/154599).  
  
3.  Aktualisieren Sie in der Liste auf der rechten Seite die folgenden Unterschlüssel.  
  
    |Unterschlüssel|Wertname|Wertdaten|  
    |----------|--------------|--------------|  
    |Screensaveactive|REG_SZ|0 (Null)|  
    |SCREENSAVETIMEOUT|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (Null)|  
  
    So aktualisieren Sie einen Registrierungs Unterschlüssel:  
  
    1.  Wenn der Registrierungsschlüssel im linken Bereich ausgewählt ist, klicken Sie im rechten Bereich mit der rechten Maustaste auf den Unterschlüssel, und klicken Sie dann auf **ändern**.  
  
    2.  Geben Sie im Dialogfeld Zeichenfolge bearbeiten einen neuen Wert in **Wertdaten**ein, und klicken Sie dann auf **OK**.  
  
4.  Nachdem Sie die Aktualisierung der Registrierungs Unterschlüssel abgeschlossen haben, starten Sie den Computer neu, um die Änderungen zu aktivieren. 
