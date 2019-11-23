---
title: Verwalten von mit NPS verwendeten Zertifikaten
description: Dieses Thema enthält Informationen zur Verwendung von Server Zertifikaten mit dem Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b83f68b52a9cceef779e5204e295bbc9e45e7a14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396197"
---
# <a name="manage-certificates-used-with-nps"></a>Verwalten von mit NPS verwendeten Zertifikaten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Wenn Sie eine Zertifikat basierte Authentifizierungsmethode wie Extensible Authentication Protocol\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\)und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 \(MS\-CHAP v2\)bereitstellen, müssen Sie ein Serverzertifikat für alle Ihre NPSS registrieren. Das Serverzertifikat muss folgende Aktionen ausführen:

- Erfüllen der Mindestanforderungen an das Serverzertifikat, wie unter [Konfigurieren von Zertifikat Vorlagen für PEAP und EAP-Anforderungen](nps-manage-cert-requirements.md) beschrieben

- Sie werden von einer Zertifizierungsstelle \(Zertifizierungsstelle\) ausgestellt, die von Client Computern als vertrauenswürdig eingestuft wird. Eine Zertifizierungsstelle ist vertrauenswürdig, wenn Ihr Zertifikat im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen für den aktuellen Benutzer und den lokalen Computer vorhanden ist.

Die folgenden Anweisungen unterstützen die Verwaltung von NPS-Zertifikaten in bereit Stellungen, bei denen die vertrauenswürdige Stamm Zertifizierungsstelle eine Drittanbieter-Zertifizierungsstelle ist, z. b. VeriSign, oder eine Zertifizierungsstelle, die Sie für Ihre Public Key-Infrastruktur \(PKI-\) mithilfe Active Directory Zertifikat Dienste \(AD CS-\)bereitgestellt haben.

## <a name="change-the-cached-tls-handle-expiry"></a>Ändern des zwischengespeicherten TLS-Handle-Ablaufs

Während der anfänglichen Authentifizierungsprozesse für EAP\-TLS, PEAP\-TLS und PEAP\-MS\-CHAP v2 speichert das NPS einen Teil der TLS-Verbindungs Eigenschaften des Verbindungs Clients zwischen. Der Client speichert außerdem einen Teil der TLS-Verbindungs Eigenschaften des NPS zwischen.

Jede einzelne Sammlung dieser TLS-Verbindungs Eigenschaften wird als TLS-Handle bezeichnet.

Client Computer können die TLS-Handles für mehrere Authentifikatoren zwischenspeichern, während NPSS die TLS-Handles vieler Client Computer zwischenspeichern kann.

Mit den zwischengespeicherten TLS-Handles auf dem Client und dem Server kann der Vorgang zur erneuten Authentifizierung schneller erfolgen. Wenn sich beispielsweise ein drahtlos Computer mit einem NPS erneut authentifiziert, kann der NPS das TLS-Handle für den drahtlosen Client untersuchen und schnell feststellen, ob die Client Verbindung eine erneute Verbindung herstellt. Der NPS autorisiert die Verbindung, ohne eine vollständige Authentifizierung durchzuführen.

Entsprechend prüft der Client das TLS-Handle für den NPS, stellt fest, dass es sich um eine erneute Verbindung handelt, und muss keine Server Authentifizierung durchführen.

Auf Computern, auf denen Windows 10 und Windows Server 2016 ausgeführt wird, beträgt der Standard Ablauf des TLS-Handles 10 Stunden.

Unter bestimmten Umständen möchten Sie möglicherweise die Ablaufzeit des TLS-Handles erhöhen oder verringern.

Beispielsweise können Sie die Ablaufzeit des TLS-Handles in Fällen verringern, in denen das Zertifikat eines Benutzers von einem Administrator widerrufen wird und das Zertifikat abgelaufen ist. In diesem Szenario kann der Benutzer weiterhin eine Verbindung mit dem Netzwerk herstellen, wenn ein NPS über ein zwischengespeichertes TLS-Handle verfügt, das noch nicht abgelaufen ist. Wenn Sie das Ablaufdatum des TLS-Handles verringern, kann dies dazu führen, dass solche Benutzer mit gesperrten Zertifikaten die Verbindung

>[!NOTE]
>Die beste Lösung für dieses Szenario besteht darin, das Benutzerkonto in Active Directory zu deaktivieren oder das Benutzerkonto aus der Active Directory Gruppe zu entfernen, der die Berechtigung zum Herstellen einer Verbindung mit dem Netzwerk in der Netzwerk Richtlinie erteilt wird. Die Weitergabe dieser Änderungen an alle Domänen Controller kann jedoch aufgrund der Replikations Latenz ebenfalls verzögert werden. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handles auf Client Computern.

Mit diesem Verfahren können Sie die Zeitspanne ändern, in der Client Computer das TLS-Handle eines NPS Zwischenspeichern. Nachdem ein NPS erfolgreich authentifiziert wurde, werden die TLS-Verbindungs Eigenschaften des NPS von Client Computern als TLS-Handle zwischengespeichert. Das TLS-Handle hat eine Standarddauer von 10 Stunden \(36 Millionen Millisekunden\). Mithilfe des folgenden Verfahrens können Sie die Ablaufzeit des TLS-Handles erhöhen oder verringern.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

>[!IMPORTANT]
>Diese Prozedur muss auf einem NPS ausgeführt werden, nicht auf einem Client Computer.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>So konfigurieren Sie die Ablaufzeit des TLS-Handles auf Client Computern

1. Öffnen Sie auf einem NPS den Registrierungs-Editor.

2. Navigieren Sie zum Registrierungsschlüssel **HKEY\_local\_machine\system\currentcontrolset\control\securityproviders\schannel**

3. Klicken Sie im Menü **Bearbeiten** auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Geben Sie **clientcachetime**ein, und drücken Sie dann die EINGABETASTE.

5. Klicken Sie mit der rechten Maustaste auf **clientcachetime**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)** .

6. Geben Sie die Zeitdauer in Millisekunden an, die Client Computer nach dem ersten erfolgreichen Authentifizierungs Versuch des NPS den TLS-Handle eines NPS zwischenspeichern soll.

## <a name="configure-the-tls-handle-expiry-time-on-npss"></a>Konfigurieren Sie die Ablaufzeit des TLS-Handles auf dem NPSS.

Verwenden Sie dieses Verfahren, um den Zeitraum zu ändern, in dem der NPSS den TLS-Handle von Client Computern zwischenspeichert. Nach der erfolgreichen Authentifizierung eines Zugriffs Clients, werden die TLS-Verbindungs Eigenschaften des Client Computers als TLS-Handle für den NPSS-Cache verwendet. Das TLS-Handle hat eine Standarddauer von 10 Stunden \(36 Millionen Millisekunden\). Mithilfe des folgenden Verfahrens können Sie die Ablaufzeit des TLS-Handles erhöhen oder verringern.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

>[!IMPORTANT]
>Diese Prozedur muss auf einem NPS ausgeführt werden, nicht auf einem Client Computer.

### <a name="to-configure-the-tls-handle-expiry-time-on-npss"></a>So konfigurieren Sie die Ablaufzeit des TLS-Handles für NPSS

1. Öffnen Sie auf einem NPS den Registrierungs-Editor.

2. Navigieren Sie zum Registrierungsschlüssel **HKEY\_local\_machine\system\currentcontrolset\control\securityproviders\schannel**

3. Klicken Sie im Menü **Bearbeiten** auf **neu**, und klicken Sie dann auf **Schlüssel**.

4. Geben Sie **ServerCacheTime**ein, und drücken Sie dann die EINGABETASTE.

5. Klicken Sie mit der rechten Maustaste auf **ServerCacheTime**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)** .

6. Geben Sie die Zeitspanne in Millisekunden ein, die der NPSS den TLS-Handle eines Client Computers nach dem ersten erfolgreichen Authentifizierungs Versuch des Clients zwischenspeichern soll.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Abrufen des SHA-1-Hashs eines vertrauenswürdigen Zertifikats der Stamm Zertifizierungsstelle

Verwenden Sie dieses Verfahren, um den SHA-1-Hash (Secure Hash Algorithmus) einer vertrauenswürdigen Stamm Zertifizierungsstelle von einem Zertifikat abzurufen, das auf dem lokalen Computer installiert ist. In einigen Fällen, z. b. beim Bereitstellen von Gruppenrichtlinie, ist es erforderlich, ein Zertifikat mit dem SHA-1-Hash des Zertifikats festzulegen.

Wenn Sie Gruppenrichtlinie verwenden, können Sie ein oder mehrere vertrauenswürdige Zertifikate der Stamm Zertifizierungsstelle angeben, die von Clients verwendet werden müssen, um den NPS während der gegenseitigen Authentifizierung mit EAP oder PEAP zu authentifizieren. Zum Festlegen eines vertrauenswürdigen Stamm Zertifizierungsstellen Zertifikats, das Clients zum Überprüfen des Serverzertifikats verwenden müssen, können Sie den SHA-1-Hash des Zertifikats eingeben.

In diesem Verfahren wird veranschaulicht, wie Sie den SHA-1-Hash eines vertrauenswürdigen Stamm Zertifizierungsstellen Zertifikats mithilfe des Microsoft Management Console (MMC)-Snap-Ins "Zertifikate" abrufen. 

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe " **Benutzer** " auf dem lokalen Computer sein.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>So rufen Sie den SHA-1-Hash eines vertrauenswürdigen Zertifikats der Stamm Zertifizierungsstelle ab

1. Geben Sie im Dialogfeld Ausführen oder in Windows PowerShell **MMC**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console \(MMC\) wird geöffnet. Klicken Sie in der MMC auf **Datei**, und klicken Sie dann auf **snap\in hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.

2. Doppelklicken Sie im Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Zertifikate**. Der Assistent für Zertifikate-Snap-in wird geöffnet. Klicken Sie auf **Computerkonto** und dann auf **Weiter**.

3. Stellen Sie sicher, dass unter **Computer auswählen** **der lokale Computer (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK**.

4. Doppelklicken Sie im linken Bereich auf **Zertifikate (lokaler Computer)** , und doppelklicken Sie dann auf den Ordner **Vertrauenswürdige Stamm Zertifizierungs** stellen.

5. Der Ordner **Zertifikate** ist ein Unterordner des Ordners **Vertrauenswürdige Stamm Zertifizierungs** stellen. Klicken Sie auf den Ordner **Zertifikate**.

6. Navigieren Sie im Detailbereich zum Zertifikat für Ihre vertrauenswürdige Stamm Zertifizierungsstelle. Doppelklicken Sie auf das Zertifikat. Das Dialogfeld **Zertifikat** wird geöffnet.

7. Klicken Sie im Dialogfeld **Zertifikat** auf die Registerkarte **Details**.

8. Scrollen Sie in der Liste der Felder zu, und wählen Sie Finger **Abdruck**aus.

9. Im unteren Bereich wird die Hexadezimalzeichenfolge angezeigt, die den SHA-1-Hash Ihres Zertifikats darstellt. Wählen Sie den SHA-1-Hash aus, und drücken Sie dann die Windows-Tastenkombination für den Kopier Befehl \(STRG\+C\), um den Hash in die Windows-Zwischenablage zu kopieren.

10. Öffnen Sie den Speicherort, an den Sie den SHA-1-Hash einfügen möchten, platzieren Sie den Cursor ordnungsgemäß, und drücken Sie dann die Windows-Tastenkombination für den Befehl einfügen, \(STRG\+V\). 

Weitere Informationen zu Zertifikaten und NPS finden Sie unter [Konfigurieren von Zertifikat Vorlagen für PEAP-und EAP-Anforderungen](nps-manage-cert-requirements.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
