---
title: Konfigurieren Sie Server automatische Registrierung von Computerzertifikaten
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: c81e85cb-ecb8-442a-ad27-442c2f9e40df
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ddf8a905fdb68bbc474b10f526b32f3d8b83af46
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Zertifikaten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

> [!NOTE]
> Bevor Sie dieses Verfahren ausführen, müssen Sie eine Serverzertifikatvorlage konfigurieren, mit dem Zertifikat Vorlagen Microsoft Management Console-Snap-in auf eine Zertifizierungsstelle, die AD CS ausgeführt wird.
Mitgliedschaften in den **Organisations-Admins** und der Stammdomäne **Domänen-Admins** Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

## <a name="configure-server-certificate-auto-enrollment"></a>Konfigurieren Sie Server automatische Registrierung von Computerzertifikaten

1. Auf dem Computer, auf dem AD DS installiert ist, öffnen Sie Windows PowerShell&reg;, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console wird geöffnet.
2. Auf der **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.
3. In **Verfügbare Snap-Ins**, führen Sie einen Bildlauf nach unten, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Die **Gruppenrichtlinienobjekt auswählen** Dialogfeld wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie auswählen **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinienverwaltung**. Wenn Sie die Option **Gruppenrichtlinienverwaltung**, Ihre Konfiguration anhand der folgenden Schritte schlägt fehl, und ein Serverzertifikat nicht wer für die Netzwerkrichtlinienserver.

4. In **Group Policy Object**, klicken Sie auf **Durchsuchen**. Die **für ein Gruppenrichtlinienobjekt Durchsuchen** Dialogfeld wird geöffnet.
5. In **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** klicken Sie auf **Default Domain Policy**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Default Domain Policy**. Erweitern Sie in der Konsole den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, und klicken Sie dann **Richtlinien öffentlicher Schlüssel**.
8. Klicken Sie auf **Richtlinien öffentlicher Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatdiensteclient - automatische Registrierung**. Die **Eigenschaften** Dialogfeld wird geöffnet. Konfigurieren Sie die folgenden Elemente, und klicken Sie dann auf **OK**:

     1. In **Konfigurationsmodell**Option **aktiviert**.
     2. Wählen Sie die **Erneuern abgelaufener Zertifikate, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** Kontrollkästchen.
     3. Wählen Sie die **Zertifikate, die Zertifikatvorlagen verwenden** Kontrollkästchen.

9. Klicken Sie auf **OK**.

## <a name="configure-user-certificate-auto-enrollment"></a>Konfigurieren der automatischen Registrierung von Zertifikaten

1. Auf dem Computer, auf dem AD DS installiert ist, öffnen Sie Windows PowerShell&reg;, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console wird geöffnet.
2. Auf der **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.
3. In **Verfügbare Snap-Ins**, führen Sie einen Bildlauf nach unten, und doppelklicken Sie auf **Gruppenrichtlinienverwaltungs-Editor**. Die **Gruppenrichtlinienobjekt auswählen** Dialogfeld wird geöffnet.

     > [!IMPORTANT]
     > Stellen Sie sicher, dass Sie auswählen **Gruppenrichtlinienverwaltungs-Editor** und nicht **Gruppenrichtlinienverwaltung**. Wenn Sie die Option **Gruppenrichtlinienverwaltung**, Ihre Konfiguration anhand der folgenden Schritte schlägt fehl, und ein Serverzertifikat nicht wer für die Netzwerkrichtlinienserver.

4. In **Group Policy Object**, klicken Sie auf **Durchsuchen**. Die **für ein Gruppenrichtlinienobjekt Durchsuchen** Dialogfeld wird geöffnet.
5. In **Domänen, Organisationseinheiten und verknüpfte Gruppenrichtlinienobjekte** klicken Sie auf **Default Domain Policy**, und klicken Sie dann auf **OK**.
6. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.
7. Doppelklicken Sie auf **Default Domain Policy**. Erweitern Sie in der Konsole den folgenden Pfad: **Benutzerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, und klicken Sie dann **Richtlinien öffentlicher Schlüssel**.
8. Klicken Sie auf **Richtlinien öffentlicher Schlüssel**. Doppelklicken Sie im Detailbereich auf **Zertifikatdiensteclient - automatische Registrierung**. Die **Eigenschaften** Dialogfeld wird geöffnet. Konfigurieren Sie die folgenden Elemente, und klicken Sie dann auf **OK**:

     1. In **Konfigurationsmodell**Option **aktiviert**.
     2. Wählen Sie die **Erneuern abgelaufener Zertifikate, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** Kontrollkästchen.
     3. Wählen Sie die **Zertifikate, die Zertifikatvorlagen verwenden** Kontrollkästchen.

9. Klicken Sie auf **OK**.

## <a name="next-steps"></a>Nächste Schritte

[Aktualisieren von Gruppenrichtlinien](refresh-group-policy.md)