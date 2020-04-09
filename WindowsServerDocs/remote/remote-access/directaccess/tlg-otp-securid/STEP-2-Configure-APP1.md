---
title: Schritt 2 App1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 19a7a4a6-9a04-42ea-a5d0-ecb28a34dbaa
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6d8720c71efba6f461aa0789fc2a143d1b1dab3f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855583"
---
# <a name="step-2-configure-app1"></a>Schritt 2 App1 konfigurieren

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Führen Sie die folgenden Schritte aus, um App1 für die OTP-Unterstützung vorzubereiten:  
  
1. Zum Erstellen und Bereitstellen einer Zertifikat Vorlage, die zum Signieren von OTP-Zertifikat Anforderungen verwendet wird. Konfigurieren Sie eine Zertifikat Vorlage zum Signieren von OTP-Zertifikat Anforderungen.  
  
2. Zum Erstellen und Bereitstellen einer Zertifikat Vorlage für OTP-Zertifikate, die von der Unternehmens Zertifizierungsstelle ausgestellt wurden. Konfigurieren Sie eine Zertifikat Vorlage für OTP-Zertifikate, die von der Unternehmens Zertifizierungsstelle ausgestellt wurden.  
  
> [!WARNING]  
> Der Entwurf dieser Test Umgebungs Anleitung umfasst Infrastruktur Server, z. b. einen Domänen Controller und eine Zertifizierungsstelle (Certification Authority, ca), die entweder Windows Server 2012 R2 oder Windows Server 2012 ausführen. Die Verwendung dieser Test Umgebungs Anleitung zum Konfigurieren von Infrastruktur Servern, auf denen andere Betriebssysteme ausgeführt werden, wurde nicht getestet, und Anweisungen zum Konfigurieren anderer Betriebssysteme sind in diesem Handbuch nicht enthalten.  
  
## <a name="to-create-and-deploy-a-certificate-template-used-to-sign-otp-certificate-requests"></a><a name="DAOTPRA"></a>So erstellen Sie eine Zertifikat Vorlage, die zum Signieren von OTP-Zertifikat Anforderungen verwendet wird  
  
1.  Führen Sie **certtmpl. msc**aus, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsole Zertifikat Vorlagen im Detailbereich mit der rechten Maustaste auf die **Computer** Vorlage, und klicken Sie auf **Doppelte Vorlage**.  
  
3.  Wählen Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Kompatibilität** in der Liste **Zertifizierungs** Stelle das gewünschte Betriebssystem aus, und klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**. Wählen Sie in der Liste **Zertifikat Empfänger** das gewünschte Betriebssystem aus, und klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.  
  
4.  Klicken Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf die Registerkarte **Allgemein** .  
  
5.  Geben Sie auf der Registerkarte **Allgemein** unter **Vorlagen Anzeige Name den Namen** **daotpra**ein. Legen Sie die **Gültigkeitsdauer** auf 2 Tage fest, und legen Sie den **Erneuerungs Zeitraum** auf 1 Tag fest. Wenn die Warnung **Zertifikat Vorlagen** angezeigt wird, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **Hinzufügen**.  
  
7.  Klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** auf **Objekttypen**. Wählen Sie im Dialogfeld **Objekttypen** die Option **Computer**aus, und klicken Sie dann auf **OK**. Geben Sie im Feld **Geben Sie die zu ausgewäfenden Objektnamen** ein den Namen **Edge1**ein, klicken Sie auf **OK**, und aktivieren Sie in der Spalte **zulassen** die Kontrollkästchen **Lesen**, **registrieren**und **automatisch registrieren** . Klicken Sie in der Spalte **zulassen** auf **Authentifizierte Benutzer**, aktivieren Sie das Kontrollkästchen **Lesen** , und deaktivieren Sie alle anderen Kontrollkästchen. Klicken Sie auf **Domänen Computer**, und deaktivieren Sie in der Spalte **zulassen** die Option **registrieren** . Klicken Sie auf **Domänen-Admins** und Organisations- **Admins** , und klicken Sie in der Spalte **zulassen** für beide auf **voll** Zugriff. Klicken Sie auf **Übernehmen**.  
  
8.  Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**. Geben Sie im **Format "Name** des Antragstellers" den Namen DNS- **Namen**ein, vergewissern Sie sich, dass das Feld **DNS-Name** aktiviert ist, **und klicken Sie**auf  
  
9. Wählen Sie auf der Registerkarte **Erweiterungen** die Option **Anwendungsrichtlinien** aus, und klicken Sie dann auf **Bearbeiten** Entfernen Sie alle vorhandenen Anwendungsrichtlinien. Klicken Sie auf **Hinzufügen**, und klicken Sie im Dialogfeld **Anwendungs Richtlinie hinzufügen** auf **neu** **, geben Sie** **im Feld** **Name** Folgendes ein, und klicken Sie auf **1.3.6.1.4.1.311.81.1.1** , und klicken Sie dann auf **OK**. Klicken Sie im Dialogfeld **Anwendungs Richtlinie hinzufügen** auf **OK**. Klicken Sie unter **Anwendungsrichtlinien Erweiterung bearbeiten**auf **OK**. Klicken Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf **OK**.  
  
## <a name="to-create-and-deploy-a-certificate-template-for-otp-certificates-issued-by-the-corporate-ca"></a><a name="DAOTPLogon"></a>So erstellen und stellen Sie eine Zertifikat Vorlage für OTP-Zertifikate bereit, die von der Unternehmens Zertifizierungsstelle ausgestellt wurden  
  
1.  Klicken Sie in der Konsole Zertifikat Vorlagen im Detailbereich mit der rechten Maustaste auf die **Smartcard-Anmelde** Vorlage, und klicken Sie auf **Doppelte Vorlage**.  
  
2.  Klicken Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Kompatibilität** in der Liste **Zertifizierungs** Stelle auf das Betriebssystem, das Sie verwenden möchten, und klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**. Wählen Sie in der Liste **Zertifikat Empfänger** das Betriebssystem aus, das Sie verwenden möchten, und klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf die Registerkarte **Allgemein** .  
  
4.  Geben Sie auf der Registerkarte **Allgemein** unter **Vorlagen Anzeige Name den Namen** **daotplogon**ein. Klicken Sie in der Dropdown Liste unter **Gültigkeitsdauer**auf **Stunden**, klicken Sie im Dialogfeld **Zertifikat Vorlagen** auf **OK**, und stellen Sie sicher, dass die Anzahl der Stunden auf 1 festgelegt ist. Geben Sie in **Erneuerungs Zeitraum**den Wert **0**ein.  
  
    > [!IMPORTANT]  
    > **Windows Server 2003**-Zertifizierungsstelle. In Fällen, in denen sich die Zertifizierungsstelle auf einem Computer befindet, auf dem Windows Server 2003 ausgeführt wird, muss die Zertifikat Vorlage auf einem anderen Computer konfiguriert werden. Dies ist erforderlich, da das Festlegen der **Gültigkeitsdauer** in Stunden nicht möglich ist, wenn Windows-Versionen vor Windows Server 2008 und Windows Vista ausgeführt werden. Wenn auf dem Computer, den Sie zum Konfigurieren der Vorlage verwenden, die Active Directory Zertifikat Dienste-Server Rolle nicht installiert ist, oder wenn es sich um einen Client Computer handelt, müssen Sie möglicherweise das Zertifikat Vorlagen-Snap-in installieren. Weitere Informationen finden Sie unter [Installieren des Zertifikat Vorlagen-Snap-Ins](https://technet.microsoft.com/library/cc732445.aspx).  
    >   
    > **Windows Server 2008 R2**-Zertifizierungsstelle. Wenn Sie bereits eine Zertifizierungsstelle (Certification Authority, ca) bereitgestellt haben, auf der Windows Server 2008 R2 ausgeführt wird, müssen Sie den **Erneuerungs Zeitraum** für die Zertifikat Vorlage auf 1 oder 2 Stunden festlegen, und der **Gültigkeits Zeitraum** muss länger sein als der **Erneuerungs Zeitraum**, aber nicht mehr als vier Stunden. Wenn Sie für eine Zertifizierungsstelle, auf der Windows Server 2008 R2 ausgeführt wird, eine **Gültigkeitsdauer** von Zertifikat Vorlagen mit einer Zertifizierungsstelle konfigurieren, die auf Windows Server R2 ausgeführt wird, kann der DirectAccess-Installations-Assistent die Zertifikat Vorlage nicht erkennen  
  
5.  Klicken Sie auf die Registerkarte **Sicherheit** , wählen Sie in der **Spalte Zulassen** die Option **Authentifizierte Benutzer**aus, und aktivieren Sie die Kontrollkästchen **Lesen** und **registrieren** . Klicken Sie auf **OK**. Klicken Sie auf **Domänen-Admins** und Organisations- **Admins**, und klicken Sie in der Spalte **zulassen** für beide auf **voll** Zugriff. Klicken Sie auf **Übernehmen**.  
  
6.  Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**. Wählen Sie im **Format** "Antragsteller Name" die Option **Vollständiger definierter Name**aus, vergewissern Sie sich, dass das Feld **Benutzer Prinzipal Name (UPN)** aktiviert ist, und klicken Sie auf übernehmen **Apply**  
  
7.  Aktivieren Sie die Registerkarte **Server** , aktivieren Sie das Kontrollkästchen keine **Zertifikate und Anforderungen in der Zertifizierungsstellen Datenbank speichern** , deaktivieren Sie das Kontrollkästchen keine Sperr **Informationen in ausgestellten Zertifikaten einschließen** , und klicken Sie dann im Dialogfeld **Eigenschaften der neuen Vorlage** auf **anwenden**.  
  
8.  Klicken Sie auf die Registerkarte Ausstellungs **Anforderungen** , aktivieren Sie das Kontrollkästchen **diese Anzahl von autorisierten Signaturen:** , und legen Sie den Wert auf 1 fest. Wählen Sie unter **Signatur den Richtlinientyp erforderlich in** der Liste die Option **Anwendungs Richtlinie**aus, und wählen Sie in der Liste **Anwendungs Richtlinie** die Option **da OTP RA**aus. Klicken Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf **OK**.  
  
9. Klicken Sie auf die Registerkarte **Erweiterungen** , und klicken Sie unter **Anwendungsrichtlinien** auf **Bearbeiten**. Löschen Sie die **Client Authentifizierung**, behalten Sie **smartcardlogon**bei, und klicken Sie zweimal auf **OK** .  
  
10. Schließen Sie die Zertifikatvorlagenkonsole.  
  
11. Geben Sie auf dem Bildschirm **Start** den**Befehl certrv. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
12. Erweitern Sie in der Konsolen Struktur der Zertifizierungsstelle **Corp-App1-ca-1**, klicken Sie auf **Zertifikat Vorlagen**, klicken Sie mit der rechten Maustaste auf **Zertifikat Vorlagen**, zeigen Sie auf **neu**, und klicken Sie dann auf Auszustellende **Zertifikat Vorlage**.  
  
13. Klicken Sie in der Liste der Zertifikat Vorlagen auf **daotpra** und **daotplogon**, und klicken Sie dann auf **OK**.  
  
14. Im Detailbereich der-Konsole sollte die **daotpra** -Zertifikat Vorlage mit dem **beabsichtigten Zweck** " **da OTP RA** " und der " **daotplogon** "-Zertifikat Vorlage mit dem **beabsichtigten Zweck** der **Smartcardanmeldung**angezeigt werden.  
  
15. Starten Sie die Dienste neu.  
  
16. Schließen Sie die Konsole Zertifizierungsstelle.  
  
17. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten. Geben Sie **certutil. exe-setreg DBFlags + DBFLAGS_ENABLEVOLATILEREQUESTS**ein, und drücken Sie die EINGABETASTE.  
  
18. Lassen Sie das Eingabe Aufforderungs Fenster für den nächsten Schritt geöffnet.  
  


