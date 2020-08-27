---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: TPM-Schlüsselnachweis
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: aa23d8df4391514d08ff1ef065af14275274dfa9
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939900"
---
# <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Eskalations Techniker mit der Windows-Gruppe

> [!NOTE]
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.

## <a name="overview"></a>Übersicht
Obwohl seit Windows 8 die Unterstützung für TPM-geschützte Schlüssel vorhanden war, gab es keine Mechanismen für Zertifizierungsstellen, die kryptografisch überzeugen, dass der private Schlüssel für die Zertifikat Anforderer tatsächlich durch einen Trusted Platform Module (TPM) geschützt ist. Diese Aktualisierung ermöglicht es einer Zertifizierungsstelle, diesen Nachweis auszuführen und diesen Nachweis im ausgestellten Zertifikat widerzuspiegeln.

> [!NOTE]
> In diesem Artikel wird davon ausgegangen, dass der Reader mit dem Zertifikat Vorlagen Konzept vertraut ist (Weitere Informationen finden Sie unter [Zertifikat Vorlagen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730705(v=ws.11))). Außerdem wird davon ausgegangen, dass der Reader mit der Konfiguration von Unternehmens Zertifizierungsstellen zum Ausstellen von Zertifikaten auf der Grundlage von Zertifikat Vorlagen vertraut ist (Weitere Informationen finden Sie unter Prüfliste: Konfigurieren von Zertifizierungsstellen [zum Ausstellen und Verwalten von Zertifikaten](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771533(v=ws.11))).

### <a name="terminology"></a>Begriff

|Begriff|Definition|
|--------|--------------|
|'|Endorsement Key. Dies ist ein asymmetrischer Schlüssel im TPM (wird zur Fertigungszeit eingefügt). Die EK ist für jedes TPM eindeutig und kann Sie identifizieren. Der EK kann nicht geändert oder entfernt werden.|
|EKpub|Bezieht sich auf den öffentlichen Schlüssel des EK-Objekts.|
|Ekpriv|Bezieht sich auf den privaten Schlüssel des EK-Objekts.|
|EKCert|EK-Zertifikat Ein vom Hersteller ausgestelltes TPM-Zertifikat für ekpub. Nicht alle TPMs haben ekcert.|
|TPM|Trusted Platform Module. Ein TPM wurde entwickelt, um hardwarebasierte sicherheitsbezogene Funktionen bereitzustellen. Ein TPM-Chip ist ein sicherer Krypto-Prozessor, der für die Ausführung kryptografischer Vorgänge ausgelegt ist. Der Chip umfasst mehrere physische Sicherheitsmechanismen, die ihn manipulationssicher machen, und Schadsoftware ist nicht in der Lage, die TPM-Sicherheitsfunktionen zu manipulieren.|

### <a name="background"></a>Hintergrund
Ab Windows 8 kann ein Trusted Platform Module (TPM) verwendet werden, um den privaten Schlüssel eines Zertifikats zu sichern. Der Schlüsselspeicher Anbieter (KSP) des Kryptografieanbieters von Microsoft ist für diese Funktion aktiviert. Bei der Implementierung gab es zwei Probleme:

-   Es gab keine Garantie dafür, dass ein Schlüssel tatsächlich durch ein TPM geschützt wird (ein Software-KSP kann problemlos als TPM-KSP mit lokalen Administrator Anmelde Informationen gespowerden).

-   Es war nicht möglich, die Liste der TPMs einzuschränken, die von einem Unternehmen ausgestellten Zertifikaten geschützt werden dürfen (falls der PKI-Administrator die Gerätetypen steuern möchte, die zum Abrufen von Zertifikaten in der Umgebung verwendet werden können).

### <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis
Mit dem TPM-Schlüssel Nachweis kann die Entität, die ein Zertifikat anfordert, einer Zertifizierungsstelle kryptografisch nachweisen, dass der RSA-Schlüssel in der Zertifikat Anforderung entweder durch ein "a" oder "das" TPM geschützt ist, dem die Zertifizierungsstelle vertraut. Das TPM-Vertrauensstellungs Modell wird weiter unten in diesem Thema im Abschnitt " [Übersicht über die Bereitstellung](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) " erläutert.

### <a name="why-is-tpm-key-attestation-important"></a>Warum ist der TPM-Schlüssel Nachweis wichtig?
Ein Benutzerzertifikat mit einem TPM-geprüften Schlüssel bietet eine höhere Sicherheitsgarantie, die durch nicht Exportierbarkeit, antihammerung und Isolation von Schlüsseln, die vom TPM bereitgestellt werden, gesichert wird.

Mit dem TPM-Schlüssel Nachweis ist nun ein neues Verwaltungs Paradigma möglich: ein Administrator kann die Gruppe von Geräten definieren, die Benutzer für den Zugriff auf Unternehmensressourcen verwenden können (z. b. VPN-oder drahtlos Zugriffspunkt) **und sicherstellen** , dass für den Zugriff auf diese Geräte keine anderen Geräte verwendet werden können. Dieses neue Zugriffs Steuerungs Paradigma ist **stark** , da es an eine *Hardware gebundene* Benutzeridentität gebunden ist, die stärker als softwarebasierte Anmelde Informationen ist.

### <a name="how-does-tpm-key-attestation-work"></a>Wie funktioniert der TPM-Schlüssel Nachweis?
Im allgemeinen basiert der TPM-Schlüssel Nachweis auf folgenden Säulen:

1.  Jedes TPM wird mit einem eindeutigen asymmetrischen Schlüssel ausgeliefert, der als *Endorsement Key* (EK) bezeichnet wird, der vom Hersteller gebrannt wurde. Der öffentliche Teil dieses Schlüssels wird als *ekpub* und der zugehörige private Schlüssel als *ekpriv*bezeichnet. Einige TPM-Chips verfügen auch über ein EK-Zertifikat, das vom Hersteller für das ekpub ausgestellt wird. Wir bezeichnen dieses Zertifikat als *ekcert*.

2.  Eine Zertifizierungsstelle richtet eine Vertrauensstellung im TPM entweder über ekpub oder ekcert ein.

3.  Ein Benutzer beweist der Zertifizierungsstelle, dass der RSA-Schlüssel, für den das Zertifikat angefordert wird, kryptografisch mit dem ekpub verknüpft ist und dass der Benutzer das ekpriv besitzt.

4.  Die Zertifizierungsstelle gibt ein Zertifikat mit einer speziellen Ausstellungs Richtlinien-OID aus, um anzugeben, dass der Schlüssel nun von einem TPM geschützt wird.

## <a name="deployment-overview"></a><a name="BKMK_DeploymentOverview"></a>Bereitstellungs Übersicht
Bei dieser Bereitstellung wird davon ausgegangen, dass eine Windows Server 2012 R2-Unternehmens Zertifizierungsstelle eingerichtet ist. Außerdem werden-Clients (Windows 8.1) für die Registrierung für die Unternehmens Zertifizierungsstelle mithilfe von Zertifikat Vorlagen konfiguriert.

Zum Bereitstellen eines TPM-Schlüssel Attestation sind drei Schritte erforderlich:

1.  **Planen Sie das TPM-Vertrauensstellungs Modell:** Der erste Schritt besteht darin, zu entscheiden, welches TPM-Vertrauens Modell verwendet werden soll. Hierfür gibt es drei Möglichkeiten:

    -   **Vertrauensstellung basierend auf den Benutzer** Anmelde Informationen: Die Unternehmens Zertifizierungsstelle vertraut dem vom Benutzer bereitgestellten ekpub als Teil der Zertifikat Anforderung, und außer den Domänen Anmelde Informationen des Benutzers wird keine Validierung ausgeführt.

    -   **Vertrauensstellung basierend auf ekcert:** Die Unternehmens Zertifizierungsstelle überprüft die ekcert-Kette, die als Teil der Zertifikat Anforderung bereitgestellt wird, an eine vom Administrator verwaltete Liste zulässiger EK-Zertifikat *Ketten*. Die zulässigen Ketten werden pro Hersteller definiert und über zwei benutzerdefinierte Zertifikat Speicher auf der ausstellenden Zertifizierungsstelle ausgedrückt (ein Speicher für die zwischengeschaltete und eine für Zertifikate der Stamm Zertifizierungsstelle). Dieser Vertrauensstellungs Modus bedeutet, dass **alle** TPMs eines bestimmten Herstellers vertrauenswürdig sind. Beachten Sie, dass in diesem Modus TPMs, die in der Umgebung verwendet werden, ekcerts enthalten müssen.

    -   **Auf ekpub basierende Vertrauensstellung:** Die Unternehmens Zertifizierungsstelle überprüft, ob die im Rahmen der Zertifikat Anforderung angegebene ekpub in einer vom Administrator verwalteten Liste zulässiger ekpubs angezeigt wird. Diese Liste wird als Verzeichnis von Dateien ausgedrückt, wobei der Name der einzelnen Dateien in diesem Verzeichnis der SHA-2-Hash der zulässigen ekpub-Datei ist. Diese Option bietet die höchste Sicherheitsstufe, erfordert jedoch mehr Verwaltungsaufwand, da jedes Gerät einzeln identifiziert wird. In diesem Vertrauens Modell können nur die Geräte, deren ekpub von TPM der Zulassungsliste von ekpubs hinzugefügt wurde, für ein TPM-attezertifikat registriert werden.

    Abhängig von der verwendeten Methode wendet die Zertifizierungsstelle eine andere Ausstellungs Richtlinien-OID auf das ausgestellte Zertifikat an. Weitere Informationen zu Ausstellungs Richtlinien OIDs finden Sie in der Tabelle "Ausstellungs Richtlinie OIDs" im Abschnitt [Konfigurieren einer Zertifikat Vorlage](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) in diesem Thema.

    Beachten Sie, dass es möglich ist, eine Kombination aus TPM-Vertrauensstellungs Modellen auszuwählen. In diesem Fall akzeptiert die Zertifizierungsstelle jede der Nachweismethoden, und die Ausstellungs Richtlinie OIDs reflektiert alle erfolgreichen Nachweismethoden.

2.  **Konfigurieren Sie die Zertifikat Vorlage:** Die Konfiguration der Zertifikat Vorlage wird im Abschnitt " [Bereitstellungs Details](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) " in diesem Thema beschrieben. In diesem Artikel wird nicht erläutert, wie diese Zertifikat Vorlage der Unternehmens Zertifizierungsstelle zugewiesen wird oder wie der Registrierungs Zugriff für eine Benutzergruppe gewährt wird. Weitere Informationen finden Sie unter Prüfliste [: Konfigurieren von CAS zum Ausstellen und Verwalten von Zertifikaten](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771533(v=ws.11)).

3.  **Konfigurieren der Zertifizierungsstelle für das TPM-Vertrauensstellungs Modell**

    1.  **Vertrauensstellung basierend auf den Benutzer** Anmelde Informationen: Eine bestimmte Konfiguration ist nicht erforderlich.

    2.  **Vertrauensstellung basierend auf ekcert:** Der Administrator muss die ekcert-Ketten Zertifikate von TPM-Herstellern abrufen und in zwei neue vom Administrator erstellte Zertifikat Speicher auf der Zertifizierungsstelle importieren, die den TPM-Schlüssel Nachweis durchführt. Weitere Informationen finden Sie im Abschnitt [ca Configuration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.

    3.  **Auf ekpub basierende Vertrauensstellung:** Der Administrator muss die ekpub-Informationen für jedes Gerät abrufen, das TPM-attezertifikate benötigt, und es der Liste der zulässigen ekpubs hinzufügen. Weitere Informationen finden Sie im Abschnitt [ca Configuration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.

    > [!NOTE]
    > -   Diese Funktion erfordert Windows 8.1/Windows Server 2012 R2.
    > -   Der TPM-Schlüssel Nachweis für Smartcard-kSPS von Drittanbietern wird nicht unterstützt. Der Kryptografieanbieter-KSP von Microsoft Platform muss verwendet werden.
    > -   Der TPM-Schlüssel Nachweis funktioniert nur für RSA-Schlüssel.
    > -   Der TPM-Schlüssel Nachweis wird für eine eigenständige Zertifizierungsstelle nicht unterstützt.
    > -   Der TPM-Schlüssel Nachweis unterstützt die [nicht persistente Zertifikat Verarbeitung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff934598(v=ws.10))nicht.

## <a name="deployment-details"></a><a name="BKMK_DeploymentDetails"></a>Bereitstellungsdetails

### <a name="configure-a-certificate-template"></a><a name="BKMK_ConfigCertTemplate"></a>Konfigurieren einer Zertifikat Vorlage
Führen Sie die folgenden Konfigurationsschritte aus, um die Zertifikat Vorlage für den TPM-Schlüssel Nachweis zu konfigurieren:

1.  Registerkarte **Kompatibilität**

    Im Abschnitt **Kompatibilitäts Einstellungen** :

    -   Stellen Sie sicher, dass für die **Zertifizierungs**Stelle **Windows Server 2012 R2** ausgewählt ist.

    -   Stellen Sie sicher, dass **Windows 8.1/Windows Server 2012 R2** für den **Zertifikat Empfänger**ausgewählt ist.

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)

2.  Registerkarte **Kryptografie**

    Stellen Sie sicher, dass der **Schlüsselspeicher Anbieter** für die **Anbieter Kategorie** ausgewählt und **RSA** als **Algorithmusname**ausgewählt ist. Stellen Sie sicher, dass **Anforderungen einen der folgenden Anbieter verwenden** ausgewählt ist und die Option **Microsoft Platform Crypto Provider** unter **Providers**ausgewählt ist.

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)

3.  Registerkarte " **Schlüssel** Nachweis"

    Dies ist eine neue Registerkarte für Windows Server 2012 R2:

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)

    Wählen Sie einen Nachweis Modus aus den drei möglichen Optionen aus.

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)

    -   **Keine:** Impliziert, dass der Schlüssel Nachweis nicht verwendet werden darf.

    -   **Erforderlich, wenn der Client fähig ist:** Ermöglicht Benutzern auf einem Gerät, das den TPM-Schlüssel Nachweis nicht unterstützt, die Anmeldung für dieses Zertifikat fortzusetzen. Benutzer, die den Nachweis durchführen können, werden mit einer speziellen Ausstellungs Richtlinien-OID unterschieden. Einige Geräte sind möglicherweise nicht in der Lage, den Nachweis aufgrund eines alten TPM auszuführen, das keinen Schlüssel Nachweis unterstützt, oder wenn das Gerät nicht über ein TPM verfügt.

    -   **Erforderlich:** Der Client *muss* einen TPM-Schlüssel Nachweis durchführen. andernfalls tritt bei der Zertifikat Anforderung ein Fehler auf.

    Wählen Sie dann das TPM-Vertrauens Modell aus. Es gibt erneut drei Optionen:

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)

    -   **Anmelde Informationen des Benutzers:** Ermöglicht einem authentifizier enden Benutzer, für ein gültiges TPM zu bürgen, indem seine Domänen Anmelde Informationen angegeben werden.

    -   **Endorsement Certificate:** Das ekcert des Geräts muss mithilfe von Administratoren verwalteten TPM-zwischen Zertifizierungsstellen-Zertifikaten für ein vom Administrator verwaltetes Stamm Zertifizierungsstellen-Zertifikat überprüft werden. Wenn Sie diese Option auswählen, müssen Sie für die ausstellende Zertifizierungsstelle ekca-und ekroot-Zertifikat Speicher wie im Abschnitt  [ca Configuration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema beschrieben einrichten.

    -   **Endorsement Key:** Der ekpub des Geräts muss in der vom Administrator verwalteten PKI-Liste angezeigt werden. Diese Option bietet die höchste Sicherheitsstufe, erfordert jedoch mehr Verwaltungsaufwand. Wenn Sie diese Option auswählen, müssen Sie eine ekpub-Liste auf der ausstellenden Zertifizierungsstelle einrichten, wie im Abschnitt [ca Configuration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema beschrieben.

    Entscheiden Sie schließlich, welche Ausstellungs Richtlinie im ausgestellten Zertifikat angezeigt werden soll. Standardmäßig verfügt jeder Erzwingungs Typ über einen zugeordneten Objekt Bezeichner (OID), der in das Zertifikat eingefügt wird, wenn er diesen Erzwingungs Typ übergibt, wie in der folgenden Tabelle beschrieben. Beachten Sie, dass es möglich ist, eine Kombination aus Erzwingungs Methoden auszuwählen. In diesem Fall akzeptiert die Zertifizierungsstelle jede der Nachweismethoden, und die Ausstellungs Richtlinien-OID reflektiert alle erfolgreichen Nachweismethoden.

    **Ausgabe Richtlinie OIDs**

    |OID|Typ des Schlüssel Nachweis|BESCHREIBUNG|Zuverlässigkeits Stufe|
    |-------|------------------------|---------------|-------------------|
    |1.3.6.1.4.1.311.21.30|'|"EK verifiziert": für die vom Administrator verwaltete Liste von EK|High|
    |1.3.6.1.4.1.311.21.31|Endorsement Certificate|"EK-Zertifikat überprüft": Wenn die EK-Zertifikat Kette überprüft wird|Medium|
    |1.3.6.1.4.1.311.21.32|Benutzeranmeldeinformationen|"Bei Verwendung von EK vertrauenswürdig": für Benutzer attetestek|Niedrig|

    Die OIDs werden in das ausgestellte Zertifikat eingefügt, wenn die Option Ausstellungs **Richtlinien einschließen** ausgewählt ist (die Standardkonfiguration).

    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)

    > [!TIP]
    > Eine mögliche Verwendung der OID im Zertifikat besteht darin, den Zugriff auf VPN oder drahtlos Netzwerke auf bestimmte Geräte zu beschränken. Beispielsweise kann Ihre Zugriffs Richtlinie die Verbindung (oder den Zugriff auf ein anderes VLAN) zulassen, wenn OID 1.3.6.1.4.1.311.21.30 im Zertifikat vorhanden ist. Dies ermöglicht es Ihnen, den Zugriff auf Geräte einzuschränken, deren TPM-EK in der ekpub-Liste vorhanden ist.

### <a name="ca-configuration"></a><a name="BKMK_CAConfig"></a>Zertifizierungsstellen Konfiguration

1.  **Einrichten von ekca-und ekroot-Zertifikat speichern auf einer ausstellenden Zertifizierungsstelle**

    Wenn Sie für die Vorlagen Einstellungen **Endorsement Certificate** ausgewählt haben, führen Sie die folgenden Konfigurationsschritte aus:

    1.  Verwenden Sie Windows PowerShell, um auf dem Server der Zertifizierungsstelle zwei neue Zertifikat Speicher zu erstellen, die einen TPM-Schlüssel Nachweis durchführen.

    2.  Abrufen der zwischen-und Stamm Zertifizierungsstellen Zertifikate von Herstellern, die Sie in ihrer Unternehmensumgebung zulassen möchten. Diese Zertifikate müssen nach Bedarf in die zuvor erstellten Zertifikat Speicher (ekca und ekroot) importiert werden.

    Mit dem folgenden Windows PowerShell-Skript werden beide Schritte ausgeführt. Im folgenden Beispiel hat der TPM-Hersteller Fabrikam ein Stamm Zertifikat *fabrikamroot. CER* und ein ausstell Endes Zertifizierungsstellen Zertifikat *fabrikamca. CER*bereitgestellt.

    ```powershell
    PS C:>\cd cert:
    PS Cert:\>cd .\\LocalMachine
    PS Cert:\LocalMachine> new-item EKROOT
    PS Cert:\ LocalMachine> new-item EKCA
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT
    ```

2.  **Einrichten der ekpub-Liste bei Verwendung des Typs "EK Nachweis"**

    Wenn Sie in den Vorlagen Einstellungen **Endorsement Key** gewählt haben, sind die nächsten Konfigurationsschritte das Erstellen und Konfigurieren eines Ordners auf der ausstellenden Zertifizierungsstelle, die 0-Byte-Dateien enthält, die jeweils für den SHA-2-Hash eines zulässigen EK benannt sind. Dieser Ordner dient als "Zulassungsliste" von Geräten, von denen TPM-Schlüssel Nachweis Zertifikate abgerufen werden können. Da Sie die ekpub-Datei für jedes Gerät, für das ein Nachweis Zertifikat erforderlich ist, manuell hinzufügen müssen, erhalten Unternehmen eine Garantie für die Geräte, die autorisiert sind, TPM-Schlüssel Nachweis Zertifikate abzurufen. Zum Konfigurieren einer Zertifizierungsstelle für diesen Modus sind zwei Schritte erforderlich:

    1.  **Erstellen Sie den Registrierungs Eintrag "endorsegmentkeylistdirectories":** Verwenden Sie das certutil-Befehlszeilen Tool, um die Ordner Orte zu konfigurieren, an denen vertrauenswürdige ekpubs definiert sind, wie in der folgenden Tabelle beschrieben.

        |Vorgang|Befehlssyntax|
        |-------------|------------------|
        |Ordner Speicherorte hinzufügen|certutil.exe-Set ca\endorgenmentkeylistdirectories + " <folder> "|
        |Ordner Speicherorte entfernen|certutil.exe-Set ca\endorgenmentkeylistdirectories-" <folder> "|

        Der endorsementkeylistdirectories im certutil-Befehl ist eine Registrierungs Einstellung, wie in der folgenden Tabelle beschrieben.

        |Wertname|Typ|Daten|
        |--------------|--------|--------|
        |Endoranmentkeylistdirectories|REG_MULTI_SZ|<lokalen oder UNC-Pfad zu ekpub-Zulassungs Listen ><p>Beispiel:<p>*\\\blueCA.contoso.com\ekpub*<p>*\\\bluecluster1.contoso.com\ekpub*<p>D:\ekpub|

        Hklm\system\currentcontrolset\services\certvc\configuration\\<CA Sanitized Name>

        *Endortskeylistdirectories* enthält eine Liste der UNC-oder lokalen Dateisystem Pfade, von denen jedes auf einen Ordner zeigt, für den die Zertifizierungsstelle über Lesezugriff verfügt. Jeder Ordner kann 0 (null) oder mehr Zulassungs Listeneinträge enthalten. jeder Eintrag ist eine Datei mit einem Namen, der der SHA-2-Hash eines vertrauenswürdigen ekpub ist, ohne Dateierweiterung.
        Das Erstellen oder Bearbeiten dieser Registrierungsschlüssel Konfiguration erfordert einen Neustart der Zertifizierungsstelle, ebenso wie vorhandene Konfigurationseinstellungen der Zertifizierungsstellen Registrierung. Änderungen an der Konfigurationseinstellung werden jedoch sofort wirksam, und es ist nicht erforderlich, dass die Zertifizierungsstelle neu gestartet wird.

        > [!IMPORTANT]
        > Sichern Sie die Ordner in der Liste vor Manipulationen und nicht autorisiertem Zugriff, indem Sie Berechtigungen so konfigurieren, dass nur autorisierte Administratoren Lese-und Schreibzugriff haben. Für das Computer Konto der Zertifizierungsstelle ist nur Lesezugriff erforderlich.

    2.  **Liste der ekpub-Liste auffüllen:** Verwenden Sie das folgende Windows PowerShell-Cmdlet, um den Hash des öffentlichen Schlüssels von TPM EK mithilfe von Windows PowerShell auf jedem Gerät abzurufen, und senden Sie den Hash des öffentlichen Schlüssels an die Zertifizierungsstelle, und speichern Sie Sie im Ordner "ekpublist".

        ```powershell
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file
        ```

## <a name="troubleshooting"></a>Problembehandlung

### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>Schlüssel Nachweis Felder sind in einer Zertifikat Vorlage nicht verfügbar.
Die Felder für den Schlüssel Nachweis sind nicht verfügbar, wenn die Vorlagen Einstellungen die Anforderungen für den Nachweis nicht erfüllen. Gängige Gründe wären etwa:

1.  Die Kompatibilitäts Einstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass Sie wie folgt konfiguriert werden:

    1.  **Zertifizierungs**Stelle: **Windows Server 2012 R2**

    2.  **Zertifikat Empfänger**: **Windows 8.1/Windows Server 2012 R2**

2.  Die Kryptografieeinstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass Sie wie folgt konfiguriert werden:

    1.  **Anbieter Kategorie**: **Schlüsselspeicher Anbieter**

    2.  **Algorithmusname**: **RSA**

    3.  **Anbieter**: **Kryptografieanbieter für Microsoft-Plattform**

3.  Die Einstellungen für die Anforderungs Behandlung sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass Sie wie folgt konfiguriert werden:

    1.  Die Option zum **Exportieren von privatem Schlüssel zulassen** darf nicht ausgewählt werden.

    2.  Die Option zum **Verschlüsseln des privaten Schlüssels des Subjekts** darf nicht ausgewählt werden.

### <a name="verification-of-tpm-device-for-attestation"></a>Überprüfung des TPM-Geräts für den Nachweis
Verwenden Sie das Windows PowerShell-Cmdlet **Confirm-caendorsementkeyinfo**, um zu überprüfen, ob ein bestimmtes TPM-Gerät für den Nachweis durch CAS vertrauenswürdig ist. Es gibt zwei Optionen: eine zum Überprüfen von ekcert und die andere für die Überprüfung eines ekpub. Das Cmdlet wird entweder lokal auf einer Zertifizierungsstelle oder auf Remote Zertifizierungsstellen mithilfe von Windows PowerShell-Remoting ausgeführt.

1.  Führen Sie die folgenden beiden Schritte aus, um die Vertrauenswürdigkeit in einem ekpub zu überprüfen:

    1.  **Extrahieren Sie die ekpub-auf dem Client Computer:** Die ekpub-Datei kann über **Get-tpmendorabmentkeyinfo**von einem Client Computer extrahiert werden. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten Folgendes aus:

        ```
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256
        ```

    2.  Über **prüfen Sie die Vertrauenswürdigkeit eines ekcert auf einem Zertifizierungsstellen Computer:** Kopieren Sie die extrahierte Zeichenfolge (SHA-2-Hash der ekpub-Datei) auf den Server (z. b. per e-Mail), und übergeben Sie Sie an das Cmdlet Confirm-caendorcmentkeyinfo. Beachten Sie, dass dieser Parameter aus 64 Zeichen bestehen muss.

        ```
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>
        ```

2.  Führen Sie die folgenden beiden Schritte aus, um die Vertrauenswürdigkeit auf einem ekcert zu überprüfen:

    1.  **Extrahieren Sie das ekcert-Zertifikat auf dem Client Computer:** Das ekcert kann über **Get-tpmendorabmentkeyinfo**von einem Client Computer extrahiert werden. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten Folgendes aus:

        ```
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```

    2.  Über **prüfen Sie die Vertrauenswürdigkeit eines ekcert auf einem Zertifizierungsstellen Computer:** Kopieren Sie das extrahierte ekcert (ekcert. cer) in die Zertifizierungsstelle (z. b. per e-Mail oder xcopy). Wenn Sie z. b. die Zertifikatsdatei in den Ordner "c:\diagnose" auf dem Zertifizierungsstellen Server kopieren, führen Sie Folgendes aus, um die Überprüfung abzuschließen:

        ```
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo
        ```

## <a name="see-also"></a>Weitere Informationen
[Übersicht über](/previous-versions/windows/it-pro/windows-8.1-and-8/jj131725(v=ws.11)) 
 Trusted Platform Module-Technologie [Externe Ressource: Trusted Platform Module](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)
