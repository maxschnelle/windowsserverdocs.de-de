---
title: Konfigurieren der automatischen Registrierung von Server Zertifikaten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: c81e85cb-ecb8-442a-ad27-442c2f9e40df
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 502e0542d326fd46a1736c08b3f34fea178b4198
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955947"
---
# <a name="configure-certificate-auto-enrollment"></a>Konfigurieren der automatischen Zertifikat Registrierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

> [!NOTE]
> Sie müssen vor der Ausführung dieses Verfahrens mithilfe des MMC-Snap-Ins Zertifikatvorlagen in einer Zertifizierungsstelle mit AD CS eine Serverzertifikatvorlage konfigurieren.
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.

## <a name="configure-server-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Server Zertifikaten

1. Öffnen Sie auf dem Computer, auf dem AD DS installiert ist, Windows PowerShell &reg; , geben Sie **MMC**ein, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.
3. Scrollen Sie in **Verfügbare Snap-Ins**nach unten, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Das Dialogfeld **Gruppenrichtlinie Objekt auswählen** wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinie Verwaltung**auswählen. Wenn Sie **Gruppenrichtlinie Verwaltung**auswählen, tritt bei der Konfiguration mit diesen Anweisungen ein Fehler auf, und ein Serverzertifikat wird nicht automatisch bei Ihrem NPSS registriert.

4. Klicken Sie in **Gruppenrichtlinienobjekt** auf **Durchsuchen**. Das Dialogfeld **Gruppenrichtlinienobjekt suchen** wird geöffnet.
5. Klicken Sie in **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** auf **Standarddomänenrichtlinie**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Standarddomänenrichtlinie**. Erweitern Sie in der-Konsole den folgenden Pfad: **Computer Konfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**und dann **Richtlinien für öffentliche Schlüssel**.
8. Klicken Sie auf **Richtlinien für öffentliche Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatsdiensteclient - automatische Registrierung**. Das Dialogfeld **Eigenschaften** wird geöffnet. Geben Sie die folgenden Elemente ein, und klicken Sie dann auf **OK**:

     1. Wählen Sie in **Konfigurationsmodell** die Option **Aktiviert** aus.
     2. Aktivieren Sie das Kontrollkästchen **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**.
     3. Aktivieren Sie das Kontrollkästchen **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren**.

9. Klicken Sie auf **OK**.

## <a name="configure-user-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Benutzer Zertifikaten

1. Öffnen Sie auf dem Computer, auf dem AD DS installiert ist, Windows PowerShell &reg; , geben Sie **MMC**ein, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.
3. Scrollen Sie in **Verfügbare Snap-Ins**nach unten, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Das Dialogfeld **Gruppenrichtlinie Objekt auswählen** wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinie Verwaltung**auswählen. Wenn Sie **Gruppenrichtlinie Verwaltung**auswählen, tritt bei der Konfiguration mit diesen Anweisungen ein Fehler auf, und ein Serverzertifikat wird nicht automatisch bei Ihrem NPSS registriert.

4. Klicken Sie in **Gruppenrichtlinienobjekt** auf **Durchsuchen**. Das Dialogfeld **Gruppenrichtlinienobjekt suchen** wird geöffnet.
5. Klicken Sie in **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** auf **Standarddomänenrichtlinie**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Standarddomänenrichtlinie**. Erweitern Sie in der-Konsole den folgenden Pfad: **Benutzerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**.
8. Klicken Sie auf **Richtlinien für öffentliche Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatsdiensteclient - automatische Registrierung**. Das Dialogfeld **Eigenschaften** wird geöffnet. Geben Sie die folgenden Elemente ein, und klicken Sie dann auf **OK**:

     1. Wählen Sie in **Konfigurationsmodell** die Option **Aktiviert** aus.
     2. Aktivieren Sie das Kontrollkästchen **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**.
     3. Aktivieren Sie das Kontrollkästchen **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren**.

9. Klicken Sie auf **OK**.

## <a name="next-steps"></a>Nächste Schritte

[Gruppenrichtlinie aktualisieren](refresh-group-policy.md)
