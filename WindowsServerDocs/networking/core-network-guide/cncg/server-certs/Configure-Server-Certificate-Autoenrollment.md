---
title: Konfigurieren Sie Server automatische Registrierung von Computerzertifikaten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: c81e85cb-ecb8-442a-ad27-442c2f9e40df
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ea7b7efe01525f4ecfb35200463c3f221d92d62d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888561"
---
# <a name="configure-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Zertifikaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

> [!NOTE]
> Bevor Sie dieses Verfahren ausführen, müssen Sie eine Zertifikatvorlage konfigurieren, indem das Zertifikat Vorlagen Microsoft Management Console-Snap-in auf eine Zertifizierungsstelle, die AD CS ausgeführt wird.
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.

## <a name="configure-server-certificate-auto-enrollment"></a>Konfigurieren Sie Server automatische Registrierung von Computerzertifikaten

1. Auf dem Computer, auf dem AD DS installiert ist, öffnen Sie Windows PowerShell&reg;, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.
3. In **Verfügbare Snap-Ins**, scrollen Sie zu, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Die **Gruppenrichtlinienobjekt auswählen** Dialogfeld wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie auswählen, **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinienverwaltung**. Bei Auswahl von **Gruppenrichtlinienverwaltung**, Ihrer Konfiguration mithilfe der Anweisungen fehl, und ein Serverzertifikat nicht automatisch registrierte, um Ihre NPSs.

4. Klicken Sie in **Gruppenrichtlinienobjekt** auf **Durchsuchen**. Das Dialogfeld **Gruppenrichtlinienobjekt suchen** wird geöffnet.
5. Klicken Sie in **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** auf **Standarddomänenrichtlinie**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Standarddomänenrichtlinie**. Erweitern Sie in der Konsole den folgenden Pfad ein: **Computerkonfiguration**, **Richtlinien**, **Windows-Einstellungen** und **Sicherheitseinstellungen**, und wählen Sie dann **Richtlinien für öffentliche Schlüssel** aus.
8. Klicken Sie auf **Richtlinien für öffentliche Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatdiensteclient - automatische Registrierung**. Die **Eigenschaften** Dialogfeld wird geöffnet. Geben Sie die folgenden Elemente ein, und klicken Sie dann auf **OK**:

     1. Wählen Sie in **Konfigurationsmodell** die Option **Aktiviert** aus.
     2. Aktivieren Sie das Kontrollkästchen **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**.
     3. Aktivieren Sie das Kontrollkästchen **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren**.

9. Klicken Sie auf **OK**.

## <a name="configure-user-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Benutzerzertifikaten

1. Auf dem Computer, auf dem AD DS installiert ist, öffnen Sie Windows PowerShell&reg;, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Microsoft Management Console wird geöffnet.
2. Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.
3. In **Verfügbare Snap-Ins**, scrollen Sie zu, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Die **Gruppenrichtlinienobjekt auswählen** Dialogfeld wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie auswählen, **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinienverwaltung**. Bei Auswahl von **Gruppenrichtlinienverwaltung**, Ihrer Konfiguration mithilfe der Anweisungen fehl, und ein Serverzertifikat nicht automatisch registrierte, um Ihre NPSs.

4. Klicken Sie in **Gruppenrichtlinienobjekt** auf **Durchsuchen**. Das Dialogfeld **Gruppenrichtlinienobjekt suchen** wird geöffnet.
5. Klicken Sie in **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** auf **Standarddomänenrichtlinie**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Standarddomänenrichtlinie**. Erweitern Sie in der Konsole den folgenden Pfad ein: **Benutzerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**.
8. Klicken Sie auf **Richtlinien für öffentliche Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatdiensteclient - automatische Registrierung**. Die **Eigenschaften** Dialogfeld wird geöffnet. Geben Sie die folgenden Elemente ein, und klicken Sie dann auf **OK**:

     1. Wählen Sie in **Konfigurationsmodell** die Option **Aktiviert** aus.
     2. Aktivieren Sie das Kontrollkästchen **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**.
     3. Aktivieren Sie das Kontrollkästchen **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren**.

9. Klicken Sie auf **OK**.

## <a name="next-steps"></a>Nächste Schritte

[Aktualisierung der Gruppenrichtlinie](refresh-group-policy.md)
