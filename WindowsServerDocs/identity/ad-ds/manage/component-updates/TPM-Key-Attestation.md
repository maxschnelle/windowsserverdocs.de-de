---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: TPM-Schlüsselnachweis
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3cfc047fe1a66617abbda1de5f2c5842dcbdeb12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862881"
---
# <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
Bei der Unterstützung für TPM-geschützten Schlüssel ist bereits seit Windows 8, gab es keine Mechanismen für Zertifizierungsstellen kryptografisch bestätigen, dass der private Schlüssel des Zertifikats-Antragsteller tatsächlich durch ein Trusted Platform Module (TPM) geschützt ist. Dieses Update ermöglicht eine Zertifizierungsstelle, Nachweis und entsprechend dieser Nachweis in das ausgestellte Zertifikat.  
  
> [!NOTE]  
> In diesem Artikel wird davon ausgegangen, dass der Leser mit dem Konzept der Zertifikat-Vorlage vertraut ist (finden Sie unter [Zertifikatvorlagen](https://technet.microsoft.com/library/cc730705.aspx)). Außerdem wird vorausgesetzt, dass der Leser mit Unternehmens-ZS zum Ausstellen von Zertifikaten basierend auf Zertifikatvorlagen konfigurieren vertraut ist (finden Sie unter [Prüfliste: Konfigurieren von Zertifizierungsstellen zum Ausstellen und Verwalten von Zertifikaten](https://technet.microsoft.com/library/cc771533.aspx)).  
  
### <a name="terminology"></a>Terminologie  
  
|Begriff|Definition|  
|--------|--------------|  
|EK|Endorsement Key. Dies ist ein asymmetrischer Schlüssel im TPM (der zur Fertigungszeit eingefügt wird). Die EK für jedes TPM eindeutig ist und sie identifizieren kann. Die EK kann nicht geändert oder entfernt werden.|  
|EKpub|Bezieht sich auf den öffentlichen Schlüssel der EK.|  
|EKPriv|Bezieht sich auf den privaten Schlüssel des der EK.|  
|EKCert|EK-Zertifikat. Ein TPM-Hersteller von ausgestelltes Zertifikat für EKPub. Nicht alle TPMs verfügen EKCert.|  
|TPM|Trusted Platform Module. Ein TPM soll hardwarebasierte sicherheitsbezogene Funktionen bereitstellen. Ein TPM-Chip ist ein sicherer Krypto-Prozessor, der für die Ausführung kryptografischer Vorgänge ausgelegt ist. Der Chip umfasst mehrere physische Sicherheitsmechanismen, die ihn manipulationssicher machen, und Schadsoftware ist nicht in der Lage, die TPM-Sicherheitsfunktionen zu manipulieren.|  
  
### <a name="background"></a>Hintergrund  
Ab Windows 8 ist ein Trusted Platform Module (TPM) dienen zum Schützen von privaten Schlüssel des Zertifikats. Die Microsoft Platform Crypto Provider Key Schlüsselspeicheranbieter (KSP) ermöglicht diese Funktion. Gab es zwei Aspekte, die die Implementierung:  

-   Gab es keine Garantie, dass ein Schlüssel tatsächlich durch ein TPM geschützt ist (jemand kann einfach eine Software-KSP als TPM KSP durch lokale Administratoranmeldeinformationen vortäuschen).

-   Es war nicht möglich, um die Liste der TPMs zu beschränken, die zum Schutz von Unternehmen, die ausgestellte Zertifikate, (wenn die PKI-Administrator die Arten von Geräten zu steuern, die zum Abrufen von Zertifikaten in der Umgebung verwendet werden kann möchte) zulässig sind.  

### <a name="tpm-key-attestation"></a>TPM-Schlüsselnachweis  
TPM-schlüsselnachweis ist die Fähigkeit der Entität, die ein Zertifikat anfordern, kryptografisch eine Zertifizierungsstelle zu beweisen, dass der RSA-Schlüssel in der zertifikatanforderung durch "a" oder "the" TPM geschützt ist, die von der Zertifizierungsstelle vertraut. Das TPM-Vertrauensmodell ausführlicher mehr die [Bereitstellungsübersicht](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) weiter unten in diesem Thema.  
  
### <a name="why-is-tpm-key-attestation-important"></a>Warum ist die TPM-schlüsselnachweis wichtig?  
Ein Zertifikat mit einem Schlüssel mit TPM-Verwendung der attested bietet höhere Sicherheit, gesichert durch nicht-Exportierbarkeit, Anti-hammering und Isolation von Schlüsseln, die vom TPM bereitgestellt.  
  
Bei TPM-schlüsselnachweisen ist jetzt ein neues Paradigma für die Verwaltung möglich: Ein Administrator kann die Gruppe von Geräten, die Benutzer verwenden können, um den Zugriff auf Unternehmensressourcen zugreifen (z. B. VPN- oder drahtlosen Zugriffspunkt) und haben definieren **starken** wird sichergestellt, dass keine weiteren Geräte verwendet werden können, um darauf zuzugreifen. Dieses neue Access-Control-Paradigma ist **starken** , da es mit verknüpft ist eine *Hardware datengebundenen* Benutzeridentität, der stärker ist als Software-basierte Anmeldeinformationen.
  
### <a name="how-does-tpm-key-attestation-work"></a>Funktionsweise von TPM-schlüsselnachweis  
Im Allgemeinen ist die folgenden Säulen TPM-schlüsselnachweis abhängig:  
  
1.  Jedes TPM ausgeliefert wird, einen eindeutigen asymmetrischen Schlüssel, dem Namen der *Endorsement Key* (EK), vom Hersteller gebrannt. Wir bezeichnen des öffentlichen Teils des Schlüssel als *EKPub* und den zugehörigen privaten Schlüssel als *EKPriv*. Eine TPM-Chips haben auch ein EK-Zertifikat, das vom Hersteller für den EKPub ausgegeben wird. Wir verweisen auf dieses Zertifikat als *EKCert*.  
  
2.  Eine Zertifizierungsstelle richtet die Vertrauensstellung im TPM EKPub oder EKCert.  
  
3.  Ein Benutzer erweist sich als an die Zertifizierungsstelle, dass der RSA-Schlüssel für den Anforderung des Zertifikats mit dem EKPub kryptografisch verknüpft ist und der Benutzer die EKpriv besitzt.  
  
4.  Die Zertifizierungsstelle ausstellt ein Zertifikat, mit einem speziellen Ausstellungsrichtlinie OID, um anzugeben, dass der Schlüssel nun nachgewiesen wird durch ein TPM geschützt werden.  
  
## <a name="BKMK_DeploymentOverview"></a>Übersicht über die Bereitstellung  
In dieser Bereitstellung wird davon ausgegangen, dass eine Windows Server 2012 R2-Unternehmenszertifizierungsstelle eingerichtet ist. Darüber hinaus Zertifikatclients (Windows 8.1) konfiguriert sind, zur Registrierung für diese Unternehmens-ZS mit Vorlagen. 

Es gibt drei Schritte zum Bereitstellen der TPM-schlüsselnachweis:  
  
1.  **Planen Sie das TPM-Vertrauensmodell:** Der erste Schritt besteht, zu entscheiden, welches TPM-Trust-Modell zu verwenden. Es gibt 3 unterstützten Möglichkeiten dafür:  
  
    -   **Die Vertrauenswürdigkeit basierend auf Anmeldeinformationen des Benutzers:** Unternehmenszertifizierungsstelle vertraut der vom Benutzer bereitgestellte EKPub im Rahmen der zertifikatanforderung, und keine Validierung wird ausgeführt als Anmeldeinformationen für die Domäne des Benutzers.  
  
    -   **Die Vertrauenswürdigkeit basierend auf EKCert:** Die Unternehmens-ZS überprüft die EKCert-Zertifikatkette, die im Rahmen der zertifikatanforderung mit einer Liste vom Administrator verwaltet, der bereitgestellt wird *akzeptable EK-Zertifikat-Ketten*. Akzeptablen Ketten, sind pro Hersteller definiert und werden auf der ausstellenden Zertifizierungsstelle (einen Speicher für die Zwischenausgabe) und eine für Zertifikate der Stammzertifizierungsstelle über zwei benutzerdefinierte Zertifikatspeicher angegeben. Dieser vertrauensstellungsmodus bedeutet, dass **alle** TPMs, die von einem angegebenen Hersteller vertrauenswürdig sind. Beachten Sie, dass in diesem Modus TPMs, die in der Umgebung EKCerts enthalten müssen.
  
    -   **Die Vertrauenswürdigkeit basierend auf EKPub:** Die Unternehmens-ZS überprüft, dass die EKPub bereitgestellt, als Teil der zertifikatanforderung in einer Liste vom Administrator verwaltet, der angezeigt wird, EKPubs zulässig. Diese Liste wird ein Verzeichnis mit Dateien angegeben, in dem der Name der einzelnen Dateien in diesem Verzeichnis den SHA-2-Hash des der zulässigen EKPub ist. Diese Option bietet die größte von Assurance jedoch mehr Verwaltungsaufwand, ist erforderlich, da jedes Gerät einzeln identifiziert wird. In diesem Vertrauensmodell dürfen nur die Geräte, die ihr TPM EKPub-Liste der zulässigen EKPubs hinzugefügt hatten ein TPM-Verwendung der attested Zertifikat registrieren.  
  
    Je nachdem, welche Methode verwendet wird wird die Zertifizierungsstelle das ausgestellte Zertifikat einen anderen Ausstellungsrichtlinie OID zuweisen. Weitere Informationen zu Ausstellungsrichtlinie OIDs, finden Sie unter der Ausstellung Richtlinie OIDs-Tabelle in der [Konfigurieren einer Zertifikatvorlage](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) in diesem Thema.  
  
    Beachten Sie, dass es möglich ist, wählen Sie eine Kombination von TPM-Trust-Modelle. In diesem Fall wird die Zertifizierungsstelle akzeptiert die Attestation-Methoden, und der Ausstellungsrichtlinie, die OIDs alle Nachweis Methoden angegeben werden, die erfolgreich ausgeführt werden.  
  
2.  **Konfigurieren der Zertifikatvorlage:** Konfigurieren der Zertifikatvorlage finden Sie auf die [Bereitstellungsdetails](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) in diesem Thema. In diesem Artikel nicht behandelt, wie diese Zertifikatvorlage die Unternehmenszertifizierungsstelle zugewiesen wird oder wie registrieren den Zugriff auf eine Gruppe von Benutzern erhält. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von Zertifizierungsstellen zum Ausstellen und Verwalten von Zertifikaten](https://technet.microsoft.com/library/cc771533.aspx).  
  
3.  **Konfigurieren Sie die Zertifizierungsstelle für das TPM-Vertrauensmodell**  
  
    1.  **Die Vertrauenswürdigkeit basierend auf Anmeldeinformationen des Benutzers:** Es ist keine spezielle Konfiguration erforderlich.  
  
    2.  **Die Vertrauenswürdigkeit basierend auf EKCert:** Der Administrator muss die EKCert-Zertifikatkette Zertifikate aus der TPM-Hersteller zu erhalten, und importieren Sie sie in zwei neue Zertifikatspeicher, durch den Administrator, bei der Zertifizierungsstelle, die TPM-schlüsselnachweis ausführen erstellt. Weitere Informationen finden Sie unter den [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    3.  **Die Vertrauenswürdigkeit basierend auf EKPub:** Der Administrator muss die EKPub für jedes Gerät abrufen, die TPM-Verwendung der attested Zertifikate benötigen und sie die Liste der zulässigen EKPubs hinzufügen. Weitere Informationen finden Sie unter den [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    > [!NOTE]  
    > -   Dieses Feature erfordert Windows 8.1 / Windows Server 2012 R2.  
    > -   TPM-schlüsselnachweis für Drittanbieter-Smartcard KSPs wird nicht unterstützt. Microsoft Platform Crypto-Provider KSP muss verwendet werden.  
    > -   TPM-schlüsselnachweis funktioniert nur für RSA-Schlüssel.  
    > -   TPM-schlüsselnachweis wird für eine eigenständige Zertifizierungsstelle nicht unterstützt.  
    > -   TPM-schlüsselnachweisen nicht unterstützt [nicht persistenter Zertifikate Verarbeitung](https://technet.microsoft.com/library/ff934598).  
  
## <a name="BKMK_DeploymentDetails"></a>Bereitstellungsdetails  
  
### <a name="BKMK_ConfigCertTemplate"></a>Konfigurieren einer Zertifikatvorlage  
Um die Zertifikatvorlage für TPM-schlüsselnachweise konfigurieren zu können, führen Sie die folgenden Konfigurationsschritte aus:  
  
1.  **Kompatibilität** Registerkarte  
  
    In der **Kompatibilitätseinstellungen** Abschnitt:  
  
    -   Stellen Sie sicher **Windows Server 2012 R2** ausgewählt ist, für die **Zertifizierungsstelle**.  
  
    -   Stellen Sie sicher **Windows 8.1 / Windows Server 2012 R2** ausgewählt ist, für die **Zertifikatsempfänger**.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **Kryptografie** Registerkarte  
  
    Stellen Sie sicher **Softwareschlüsselspeicher-Anbieter** ausgewählt ist, für die **Anbieterkategorie** und **RSA** ausgewählt ist die **Algorithmusname**. Stellen Sie sicher **Anforderungen müssen eine der folgenden Anbieter verwenden** ausgewählt ist und die **Kryptografieanbieter für Microsoft-Plattform** ausgewählt ist unter **Anbieter**.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **Schlüsselnachweis** Registerkarte  
  
    Dies ist eine neue Registerkarte für Windows Server 2012 R2:  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    Wählen Sie eine nachweismodus, der drei möglichen Optionen.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **None:** Bedeutet, dass es sich bei den schlüsselnachweis nicht verwendet werden muss  
  
    -   **Erforderlich, wenn der Client kann:** Ermöglicht Benutzern auf einem Gerät, das TPM-schlüsselnachweis zum Fortsetzen der Registrierung für dieses Zertifikat nicht unterstützt. Benutzer, die Nachweis durchführen können, werden mit einer speziellen Ausstellungsrichtlinie OID unterschieden werden. Einige Geräte sind möglicherweise nicht in der Nachweis aufgrund einer alten TPM ausführen, die den schlüsselnachweis oder das Gerät nicht auf allen über ein TPM nicht unterstützt.
  
    -   **Erforderlich:** Client *müssen* führen Sie TPM-schlüsselnachweise, andernfalls schlägt die Anforderung fehl.  
  
    Wählen Sie dann das TPM-Vertrauensmodell. Es stehen drei Optionen:  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **Anmeldeinformationen des Benutzers:** Können Sie einen authentifizierenden Benutzers zu durch Angabe ihrer Anmeldeinformationen für die Domäne für eine gültige TPM zu bestätigen.  
  
    -   **Endorsement-Zertifikat:** Der EKCert des Geräts muss über vom Administrator verwaltet TPM Zwischenzertifizierungsstellen-Zertifikate auf ein vom Administrator verwaltet Stamm-CA-Zertifikat überprüfen. Wenn Sie diese Option auswählen, müssen Sie einrichten EKCA und EKRoot Zertifikatspeichern auf der ausstellenden Zertifizierungsstelle, unter der [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    -   **Endorsement Key:** Die EKPub des Geräts muss in der Liste für die PKI-Administrator verwaltete angezeigt werden. Diese Option bietet die größte von Assurance jedoch mehr Verwaltungsaufwand erfordert. Wenn Sie diese Option auswählen, müssen Sie Einrichten einer EKPub-Liste auf der ausstellenden Zertifizierungsstelle wie beschrieben in der [Zertifizierungsstellenkonfiguration](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in diesem Thema.  
  
    Zum Schluss entscheiden Sie, welche Ausstellungsrichtlinie in das ausgestellte Zertifikat angezeigt. Standardmäßig verfügt jede über Erzwingung eine zugeordnete Objekt-ID (OID), der in das Zertifikat eingefügt wird, wenn er dieses Typs Erzwingung besteht, wie in der folgenden Tabelle beschrieben. Beachten Sie, dass es möglich ist, eine Kombination von Erzwingungsmethoden wählen. In diesem Fall die Zertifizierungsstelle wird einer der Methoden Nachweis akzeptiert, und der Ausstellungsrichtlinie OID wird alle Attestation-Methoden, die erfolgreich angewendet.  
  
    **Die Richtlinie OIDs Ausstellung**  
  
    |OID|Typ für den schlüsselnachweis|Beschreibung|Vertrauensgrad|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK überprüft":   Vom Administrator verwaltet Liste EK|Hoch|  
    |1.3.6.1.4.1.311.21.31|Endorsement-Zertifikat|"EK-Zertifikat überprüft": Wann wird EK-Zertifikatskette validiert.|Mittel|  
    |1.3.6.1.4.1.311.21.32|Benutzeranmeldeinformationen|"Vertrauenswürdige EK bei der Verwendung": Für Benutzer-Verwendung der attested EK|Niedrig|  
  
    Die OIDs werden in das ausgestellte Zertifikat eingefügt werden, wenn **Ausstellungsrichtlinien enthalten** ist (die Standardkonfiguration) ausgewählt.  
  
    ![TPM-Schlüsselnachweis](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > Eine mögliche Verwendung müssen die OID, die im Zertifikat vorhanden ist zum Einschränken des Zugriffs mit VPN oder drahtlose Netzwerke für bestimmte Geräte. Ihre Access-Richtlinie kann z. B. Verbindung (oder den Zugriff auf ein anderes VLAN) zulassen, wenn OID 1.3.6.1.4.1.311.21.30 im Zertifikat vorhanden ist. Dadurch können Sie den Zugriff auf Geräte einschränken, deren TPM EK in der EKPUB-Liste vorhanden ist.  
  
### <a name="BKMK_CAConfig"></a>Konfiguration der Zertifizierungsstelle  
  
1.  **Einrichten einer ausstellenden Zertifizierungsstelle EKCA und EKROOT Zertifikatspeicher**  
  
    Wenn Sie ausgewählt haben **Endorsement-Zertifikat** Vorlageneinstellungen, führen Sie die folgenden Konfigurationsschritte aus:  
  
    1.  Verwenden Sie Windows PowerShell, um zwei neue Zertifikatspeicher auf dem Server der Zertifizierungsstelle (CA) zu erstellen, die TPM-schlüsselnachweis ausgeführt werden.  
  
    2.  Abrufen der temporäre und Stamm-ZS-Zertifikate von Manufacturer(s), die Sie in Ihrer unternehmensumgebung zulassen möchten. Diese Zertifikate müssen in der zuvor erstellten Zertifikatspeicher (EKCA EKROOT) nach Bedarf importiert werden.  
  
    Das folgende Windows PowerShell-Skript führt beide der folgenden Schritte aus. Im folgenden Beispiel stellt die TPM-Hersteller Fabrikam ein Stammzertifikat *FabrikamRoot.cer* und eines Zertifizierungsstellenzertifikats der ausstellenden *Fabrikamca.cer*.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **Einrichten von EKPUB-Liste, wenn EK-Nachweis-Typ verwenden**  
  
    Wenn Sie ausgewählt haben **Endorsement Key** in den Vorlageneinstellungen die nächsten Konfigurationsschritte, die zum Erstellen und konfigurieren einen Ordner auf der ausstellenden Zertifizierungsstelle, die mit 0-Byte-Dateien sind, jeweils mit dem Namen für den SHA-2-Hash, der eine zulässige EK. Dieser Ordner dient als eine "Liste der zugelassenen" von Geräten, die zum Abrufen der TPM-Key-Verwendung der attested Zertifikate zulässig sind. Da Sie manuell die EKPUB für jedes einzelne Gerät, die ein attested Zertifikat erfordert hinzufügen müssen, bietet es Unternehmen eine Garantie der Geräte, die autorisiert sind, um TPM-Verwendung der attested Zertifikate zu erhalten. Konfigurieren von einer Zertifizierungsstelle in diesem Modus sind zwei Schritte erforderlich:  
  
    1.  **Erstellen Sie den Registrierungseintrag EndorsementKeyListDirectories:** Verwenden Sie das Befehlszeilentool "Certutil" So konfigurieren Sie die Ordnerpfade, in der vertrauenswürdigen EKpubs definiert sind, wie in der folgenden Tabelle beschrieben.  
  
        |Vorgang|Befehlssyntax|  
        |-------------|------------------|  
        |Hinzufügen von Ordnern|Certutil.exe - Setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |Entfernen Sie die Speicherorte von Ordnern|Certutil.exe - Setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Die EndorsementKeyListDirectories im Befehl "Certutil" ist eine registrierungseinstellung, wie in der folgenden Tabelle beschrieben.  
  
        |Wertname|Typ|Daten|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< lokaler oder UNC-Pfad zur EKPUB zulassen (n) ><br /><br />Beispiel:<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories* enthält eine Liste der UNC- oder lokale Dateisystempfade, die jeweils auf einen Ordner mit die Zertifizierungsstelle Lesezugriff auf zeigen. Jeder Ordner kann 0 (null) enthalten oder mehr zugelassen Einträge aufzulisten, ist jeder Eintrag eine Datei mit einem Namen, den SHA-2-Hash von einem vertrauenswürdigen EKpub, ohne Dateierweiterung. 
        Erstellen oder Bearbeiten von dieser Konfiguration ist einen Neustart der Zertifizierungsstelle, wie vorhandene Configuration registrierungseinstellungen der Zertifizierungsstelle erforderlich. Allerdings Änderungen an der Konfigurationseinstellung werden sofort wirksam und müssen sich nicht auf die Zertifizierungsstelle neu gestartet werden.  
  
        > [!IMPORTANT]  
        > Sichern die Ordner in der Liste vor Manipulationen und nicht autorisierten Zugriff durch Konfigurieren von Berechtigungen, sodass nur autorisierte Administratoren verfügen über Lese- und Schreibzugriff. Das Computerkonto der Zertifizierungsstelle ist nur Lesezugriff erforderlich.  
  
    2.  **Füllen Sie die EKPUB-Liste:** Verwenden Sie das folgende Windows PowerShell-Cmdlet den Hash für öffentliche Schlüssel von der TPM EK mithilfe von Windows PowerShell auf jedem Gerät zu erhalten und diesen Hash für öffentliche Schlüssel der Zertifizierungsstelle zu senden, und speichern Sie sie auf den Ordner "EKPubList".  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>Problembehandlung  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>Felder für den schlüsselnachweis sind nicht verfügbar für eine Zertifikatvorlage  
Die Schlüsselnachweis Felder sind nicht verfügbar, wenn die Vorlageneinstellungen die Anforderungen für den Nachweis nicht erfüllen. Häufige Ursachen sind:  
  
1.  Die kompatibilitätseinstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  **Zertifizierungsstelle**: **Windows Server 2012 R2**  
  
    2.  **Zertifikat-Empfänger**: **Windows 8.1/Windows Server 2012 R2**  
  
2.  Die Kryptografieeinstellungen sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  **Anbieterkategorie**: **Softwareschlüsselspeicher-Anbieter**  
  
    2.  **Name des Algorithmus**: **RSA**  
  
    3.  **Anbieter**: **Kryptografieanbieter für Microsoft-Plattform**  
  
3.  Die Einstellungen für die Behandlung der Anforderung sind nicht ordnungsgemäß konfiguriert. Stellen Sie sicher, dass sie wie folgt konfiguriert werden:  
  
    1.  Die **privatem Schlüssel zulassen zu exportierenden** Option nicht ausgewählt werden muss.  
  
    2.  Die **privaten Schlüssel des Antragstellers Verschlüsselung archivieren** Option nicht ausgewählt werden muss.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>Überprüfung der TPM-Geräts für den Nachweis  
Verwenden Sie das Windows PowerShell-Cmdlet **Confirm-CAEndorsementKeyInfo**, um sicherzustellen, dass ein bestimmtes TPM-Gerät für den Nachweis von CAs als vertrauenswürdig eingestuft wird. Es gibt zwei Optionen: eine für die Überprüfung der EKCert und die andere zum Überprüfen einer EKPub. Das Cmdlet wird entweder lokal auf einer Zertifizierungsstelle oder remote CAs ausführen mithilfe von Windows PowerShell-Remoting.  
  
1.  Führen Sie zum Überprüfen auf eine EKPub Vertrauenswürdigkeit, die folgenden beiden Schritte aus:  
  
    1.  **Extrahieren Sie die EKPub vom Clientcomputer aus:** Die EKPub extrahiert werden kann, von einem Clientcomputer über **Get-TpmEndorsementKeyInfo**. Führen Sie eine Eingabeaufforderung mit erhöhten Rechten Folgendes ein:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **Überprüfen Sie die Vertrauenswürdigkeit auf einem EKCert auf einem Zertifizierungsstellencomputer:** Kopieren Sie die extrahierte Zeichenfolge (der SHA-2-Hash der EKPub) auf den Server (z. B. per e-Mail), und übergeben Sie es an das Cmdlet "Confirm-CAEndorsementKeyInfo". Beachten Sie, dass dieser Parameter auf 64 Zeichen lang sein muss.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  Führen Sie zum Überprüfen auf eine EKCert Vertrauenswürdigkeit, die folgenden beiden Schritte aus:  
  
    1.  **Extrahieren Sie die EKCert vom Clientcomputer aus:** Der EKCert extrahiert werden kann, von einem Clientcomputer über **Get-TpmEndorsementKeyInfo**. Führen Sie eine Eingabeaufforderung mit erhöhten Rechten Folgendes ein:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **Überprüfen Sie die Vertrauenswürdigkeit auf einem EKCert auf einem Zertifizierungsstellencomputer:** Kopieren Sie den extrahierten EKCert (EkCert.cer) an die Zertifizierungsstelle (z. B. über e-Mail oder Xcopy). Wenn Sie die Zertifikatdatei den Ordner "c:\diagnose" auf dem Zertifizierungsstellenserver kopieren, führen Sie beispielsweise Folgendes ein, um die Überprüfung abzuschließen:  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>Siehe auch  
[Trusted Platform Module – Technologieübersicht](https://technet.microsoft.com/library/jj131725.aspx)  
[Externe Ressource: Trusted Platform Module](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
