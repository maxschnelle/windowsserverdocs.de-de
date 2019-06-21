---
title: Schritt 2 Konfigurieren von APP1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19a7a4a6-9a04-42ea-a5d0-ecb28a34dbaa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 093f8215691b21d7b7fefc3b1c51f3a41af9bea6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283134"
---
# <a name="step-2-configure-app1"></a>Schritt 2 Konfigurieren von APP1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um APP1 für die Unterstützung von OTP vorzubereiten:  
  
1. Fordert zum Erstellen und Bereitstellen einer Zertifikatvorlage verwendet, um die OTP-Zertifikat zu signieren. Konfigurieren Sie eine Zertifikatvorlage, die zum Signieren von OTP zertifikatsanforderungen verwendet.  
  
2. Zum Erstellen und Bereitstellen einer Zertifikatvorlage für OTP-Zertifikate, die von der Zertifizierungsstelle des Unternehmens ausgestellt. Konfigurieren Sie eine Zertifikatvorlage für OTP-Zertifikate, die von der Zertifizierungsstelle des Unternehmens ausgestellt.  
  
> [!WARNING]  
> Das Design der vorliegenden testumgebungsanleitung enthält Infrastrukturserver, z. B. einen Domänencontroller und einer Zertifizierungsstelle (CA), die entweder Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden. Mit der vorliegenden testumgebungsanleitung Infrastrukturserver zu konfigurieren, auf denen andere Betriebssysteme ausgeführt werden nicht getestet wurde, und Anweisungen zum Konfigurieren von anderen Betriebssystemen sind in dieser Anleitung nicht enthalten.  
  
## <a name="DAOTPRA"></a>Erstellen und Bereitstellen einer Zertifikatvorlage, die zum Signieren von OTP-zertifikatanforderungen  
  
1.  Führen Sie **certtmpl.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Die Zertifikatvorlagenkonsole, klicken Sie im Detailbereich mit der Maustaste der **Computer** Vorlage, und klicken Sie auf **Doppelte Vorlage**.  
  
3.  Auf der **Eigenschaften der neuen Vorlage** Dialogfeld auf die **Kompatibilität** Registerkarte die **Zertifizierungsstelle** wählen Sie das Betriebssystem, Sie möchten, und in der  **Resultierende Änderungen** Dialogfeld auf **OK**. In der **Zertifikatsempfänger** Liste Wählen Sie das Betriebssystem, Sie möchten, und klicken Sie in der **resultierende Änderungen** Dialogfeld auf **OK**.  
  
4.  Auf der **Eigenschaften der neuen Vorlage** Dialogfeld klicken Sie auf die **allgemeine** Registerkarte.  
  
5.  Auf der **allgemeine** Registerkarte **Vorlagenanzeigename**, Typ **DAOTPRA**. Legen Sie die **Gültigkeitsdauer** auf 2 Tage, und legen die **Erneuerungszeitraum** von 1 Tag. Wenn die **Zertifikatvorlagen** Warnung wird angezeigt, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Hinzufügen**.  
  
7.  Auf der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** Dialogfeld klicken Sie auf **Objekttypen**. Auf der **Objekttypen** wählen Sie im Dialogfeld **Computer**, und klicken Sie dann auf **OK**. In der **Geben Sie die zu verwendenden Objektnamen** geben **EDGE1**, klicken Sie auf **OK**, und klicken Sie in der **zulassen** Spalte die **lesen** , **Registrieren**, und **automatisch registrieren** Kontrollkästchen. Klicken Sie auf **authentifizierte Benutzer**, wählen die **lesen** Kontrollkästchen unter der **zulassen** Spalte, und alle anderen Kontrollkästchen zu deaktivieren. Klicken Sie auf **Domänencomputer**, und deaktivieren Sie **registrieren** unter der **zulassen** Spalte. Klicken Sie auf **Domänen-Admins** und **Organisations-Admins** , und klicken Sie auf **Vollzugriff** unter der **zulassen** Spalte für beide. Klicken Sie auf **Übernehmen**.  
  
8.  Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**. In der **Format des Antragstellernamens:** Liste wählen **DNS-Namen**, stellen Sie sicher, dass die **DNS-Namen** Kontrollkästchen aktiviert ist, und klicken Sie auf **übernehmen**.  
  
9. Klicken Sie auf die **Erweiterungen** Registerkarte **Anwendungsrichtlinien** , und klicken Sie dann auf **bearbeiten**. Entfernen Sie alle vorhandenen Anwendungsrichtlinien. Klicken Sie auf **hinzufügen**, und klicken Sie auf die **Anwendungsrichtlinie hinzufügen** Dialogfeld klicken Sie auf **neu**, geben Sie **DA OTP RA** in die **Name:** Feld und **1.3.6.1.4.1.311.81.1.1** in die **Objekt-ID:** ein, und klicken Sie auf **OK**. Auf der **Anwendungsrichtlinie hinzufügen** Dialogfeld klicken Sie auf **OK**. Auf der **Anwendungsrichtlinienerweiterung**, klicken Sie auf **OK**. Auf der **Eigenschaften der neuen Vorlage** Dialogfeld klicken Sie auf **OK**.  
  
## <a name="DAOTPLogon"></a>Erstellen und Bereitstellen einer Zertifikatvorlage für OTP-Zertifikate, die von der Zertifizierungsstelle des Unternehmens ausgestellt  
  
1.  Die Zertifikatvorlagenkonsole, klicken Sie im Detailbereich mit der Maustaste der **Smartcard-Anmeldung** Vorlage, und klicken Sie auf **Doppelte Vorlage**.  
  
2.  Auf der **Eigenschaften der neuen Vorlage** Dialogfelds die **Kompatibilität** Registerkarte die **Zertifizierungsstelle** Liste, klicken Sie auf das Betriebssystem, das Sie verwenden möchten, und klicken Sie in der **Resultierende Änderungen** Dialogfeld klicken Sie auf **OK**. In der **Zertifikatsempfänger** Liste Wählen Sie das Betriebssystem, das Sie verwenden möchten, und klicken Sie in der **resultierende Änderungen** Dialogfeld auf **OK**.  
  
3.  Auf der **Eigenschaften der neuen Vorlage** Dialogfeld klicken Sie auf die **allgemeine** Registerkarte.  
  
4.  Auf der **allgemeine** Registerkarte **Vorlagenanzeigename**, Typ **DAOTPLogon**. In **Gültigkeitsdauer**, in der Dropdown-Liste, klicken Sie auf **Stunden**auf die **Zertifikatvorlagen** Dialogfeld klicken Sie auf **OK**, und stellen Sie sicher, dass dass die Anzahl der Stunden auf 1 festgelegt ist. In **Erneuerungszeitraum**, Typ **0**.  
  
    > [!IMPORTANT]  
    > **Windows Server 2003 CA**. In Situationen, in denen die Zertifizierungsstelle (CA) auf einem Computer, auf denen Windows Server 2003 ausgeführt wird, muss die Zertifikatvorlage klicken Sie dann auf einem anderen Computer konfiguriert werden. Dies ist erforderlich, da das Festlegen der **Gültigkeitsdauer** in Stunden ist nicht möglich, wenn Windows-Versionen vor Windows Server 2008 und Windows Vista ausgeführt wird. Wenn der Computer, mit denen Sie die Vorlage zu konfigurieren, verfügt nicht über die Active Directory Certificate Services-Serverrolle installiert, oder wenn es sich um einen Client-Computer ist, dann Sie möglicherweise das Zertifikatvorlagen-Snap-in zu installieren müssen. Weitere Informationen finden Sie unter [installieren, die Zertifikatvorlagen-Snap-Ins](https://technet.microsoft.com/library/cc732445.aspx).  
    >   
    > **Windows Server 2008 R2 CA**. Wenn Sie eine Zertifizierungsstelle (CA), auf denen Windows Server 2008 R2 ausgeführt wird, bereits bereitgestellt haben, müssen Sie konfigurieren, dass die Zertifikatvorlage **Erneuerungszeitraum** auf 1 oder 2 Stunden und die **Gültigkeitsdauer** auf nicht länger als die **Erneuerungszeitraum**, aber nicht mehr als 4 Stunden. Wenn Sie eine Zertifikatvorlage konfigurieren **Gültigkeitsdauer** der länger als vier Stunden mit einer Zertifizierungsstelle, die Windows Server 2008 R2 ausgeführt wird, nicht der DirectAccess-Installations-Assistenten erkannt, die Zertifikatvorlage aus, und klicken Sie auf DirectAccess Fehler bei der Installation.  
  
5.  Klicken Sie auf die **Sicherheit** Registerkarte **authentifizierte Benutzer**in die **zulassen** Spalte, und wählen die **lesen** und **registrieren**  Kontrollkästchen. Klicken Sie auf **OK**. Klicken Sie auf **Domänen-Admins** und **Organisations-Admins**, und klicken Sie auf **Vollzugriff** unter der **zulassen** Spalte für beide. Klicken Sie auf **Übernehmen**.  
  
6.  Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**. In der **Format des Antragstellernamens:** Liste wählen **Vollständiger definierter Name**, stellen Sie sicher, dass die **Benutzerprinzipalname (UPN)** Kontrollkästchen aktiviert ist, und klicken Sie auf **anwenden** .  
  
7.  Klicken Sie auf die **Server** Registerkarte die **Zertifikate und Anforderungen nicht in der Datenbank der Zertifizierungsstelle speichern** deaktivieren Sie das Kontrollkästchen der **beinhalten keine Informationen zum Widerrufen in ausgestellten Zertifikaten** Kontrollkästchen, und klicken Sie dann auf die **Eigenschaften der neuen Vorlage** Dialogfeld klicken Sie auf **übernehmen**.  
  
8.  Klicken Sie auf die **Ausstellungsvoraussetzungen** Registerkarte die **diese Anzahl an autorisierten Signaturen:** Kontrollkästchen, die den Wert auf 1 festgelegt. In der **Signatur Erforderlicher Richtlinientyp:** Liste wählen **Anwendungsrichtlinie**, und klicken Sie in der **Anwendungsrichtlinie** Liste wählen **DA OTP RA**. Auf der **Eigenschaften der neuen Vorlage** Dialogfeld klicken Sie auf **OK**.  
  
9. Klicken Sie auf die **Erweiterungen** Registerkarte, und klicken Sie auf **Anwendungsrichtlinien** klicken Sie auf **bearbeiten**. Löschen Sie **Clientauthentifizierung**, behalten Sie **SmartCardLogon**, und klicken Sie auf **OK** zweimal.  
  
10. Schließen Sie die Zertifikatvorlagenkonsole.  
  
11. Auf der **starten** geben**certsrv.msc**, und drücken Sie dann die EINGABETASTE.  
  
12. Erweitern Sie in der Konsolenstruktur der Zertifizierungsstelle **corp-APP1-CA-1**, klicken Sie auf **Zertifikatvorlagen**, mit der rechten Maustaste **Zertifikatvorlagen**, zeigen Sie auf **Neu**, und klicken Sie auf **Auszustellende Zertifikatvorlage**.  
  
13. In der Liste der Zertifikatvorlagen, klicken Sie auf **DAOTPRA** und **DAOTPLogon**, und klicken Sie auf **OK**.  
  
14. Im Detailbereich der Konsole angezeigt der **DAOTPRA** Zertifikatvorlage mit einer **Beabsichtigter Zweck** von **DA OTP RA** und **DAOTPLogon** Zertifikatvorlage mit einer **Beabsichtigter Zweck** von **Smartcard-Anmeldung**.  
  
15. Starten Sie die Dienste neu.  
  
16. Schließen Sie die Zertifizierungsstellenkonsole.  
  
17. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten. Typ **CertUtil.exe - SetReg DBFlags + DBFLAGS_ENABLEVOLATILEREQUESTS**, und drücken Sie EINGABETASTE.  
  
18. Lassen Sie das Eingabeaufforderungsfenster geöffnet, für den nächsten Schritt.  
  


