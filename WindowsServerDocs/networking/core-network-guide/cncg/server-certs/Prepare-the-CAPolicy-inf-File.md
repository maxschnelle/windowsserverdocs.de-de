---
title: Vorbereiten der CAPolicy.inf-Datei
description: Die CAPolicy.inf enthält verschiedene Einstellungen, die bei der Installation der Active Directory-Zertifizierung-Dienst (AD CS) oder beim Erneuern der Zertifizierungsstelle verwendet werden Zertifikat.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9618d4abe512b487f4f22ffde85a052c1c52ef22
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf-Syntax
>   Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die CAPolicy.inf ist eine Konfigurationsdatei, die definiert, die Erweiterungen, Einschränkungen und anderen Konfigurationseinstellungen, die auf ein Zertifikat einer Stammzertifizierungsstelle und alle von der Stamm-ZS ausgestellten Zertifikate angewendet werden. Die CAPolicy.inf-Datei muss auf einem Hostserver, bevor Sie die Setuproutine für den Stamm installiert werden, beginnt der Zertifizierungsstelle. Wenn die sicherheitseinschränkungen auf einer Stamm-ZS sind geändert werden, muss das Stammzertifizierungsstellen-Zertifikat erneuert werden, und eine aktualisierte CAPolicy.inf-Datei muss auf dem Server installiert werden, bevor der Prozess der Verlängerung beginnt.

Die CAPolicy.inf ist:

-   Erstellt und manuell vom Administrator definierte

-   Während der Erstellung von Stammzertifizierungsstellen und untergeordnete ZS-Zertifikate

-   Definiert die signierenden Zertifizierungsstelle, in dem Sie sich anmelden, und stellen Sie das Zertifikat (nicht die Zertifizierungsstelle, in dem die Anforderung gewährt wird)

Nachdem Sie die CAPolicy.inf-Datei erstellt haben, müssen Sie kopieren Sie ihn in die **SystemRoot%** Ordner des Servers vor der Installation MDE oder Erneuern des Zertifikats der Zertifizierungsstelle.

Die CAPolicy.inf ermöglicht das angeben und eine Vielzahl von Zertifizierungsstellen und -Optionen konfigurieren. Im folgenden Abschnittwerden alle Optionen für Sie erstellen eine INF-Datei an Ihre Bedürfnisse angepasst sind.

## <a name="capolicyinf-file-structure"></a>Struktur der CAPolicy.inf-Datei

Die folgenden Begriffe werden verwendet, um die Struktur der INF-Datei zu beschreiben:

-   _Abschnitt_ – ist ein Bereich der Datei, die eine logische Gruppe von Tasten behandelt. Abschnittsnamen in der INF-Dateien werden in Klammern angezeigt werden identifiziert. Viele, aber nicht für alle Abschnitte dienen zum zertifikaterweiterungen konfigurieren.

-   _Schlüssel_ – ist der Name eines Eintrags und auf der linken Seite des Gleichheitszeichens wird angezeigt.

-   _Wert_ – ist der Parameter und rechts neben dem Gleichheitszeichen angezeigt wird.

Im folgenden Beispiel **[Version]** ist der Abschnitt **Signatur** ist der Schlüssel und **"\ $ Windows NT \ $"** ist der Wert.

Beispiel:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>Version

Gibt die Datei als INF-Datei. Version ist der einzige Abschnitterforderlich und muss zu Beginn der CAPolicy.inf-Datei sein.

###  <a name="policystatementextension"></a>PolicyStatementExtension

Sind die Richtlinien aufgeführt, die von der Organisation definiert wurden und ob diese optional oder obligatorisch sind. Mehrere Richtlinien werden durch Kommas getrennt. Die Namen werden im Kontext einer bestimmten Bereitstellung oder in Bezug auf benutzerdefinierte Anwendungen, die Überprüfung auf das Vorhandensein dieser Richtlinien Bedeutung haben.

Für jede Richtlinie definiert ist muss ein Abschnitt, der die Einstellungen für diese bestimmte Richtlinie definiert sein. Für jede Richtlinie müssen Sie eine benutzerdefinierte objektkennung (OID) angeben, und der Text angezeigt werden sollen als die richtlinienanweisung oder ein URL-Zeiger auf die richtlinienanweisung. Die URL kann in Form einer HTTP, FTP oder LDAP-URL sein.

Wenn Sie beabsichtigen, haben einen beschreibenden Text in den Richtlinien, würde die nächsten drei Zeilen der der CAPolicy.inf wie aussehen:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

Wenn Sie beabsichtigen, eine URL zu verwenden, um die CA-Policy-Anweisung zu hosten, sieht wie stattdessen nächsten drei Zeilen aus:

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
```

Außerdem:

-   Mehrere URLs und beachten Sie Schlüssel werden unterstützt.

-   Hinweis und URL-Schlüssel im gleichen Abschnittder Richtlinie werden unterstützt.

-   URLs und Text mit Leerzeichen muss in Anführungszeichen gesetzt werden. Dies gilt für die **URL** Key, unabhängig von den Abschnitt, in dem es angezeigt wird.

Ein Beispiel für mehrere Notizen und URLs in einem Richtlinienabschnitt aussehen würde:

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Sie können Zertifikatsperrlisten-Verteilungspunkte (CDP) für ein Zertifikat einer Stammzertifizierungsstelle in der CAPolicy.inf angeben. Nach der Installation der Zertifizierungsstelle können Sie die URLs für CDP konfigurieren, die in jedem ausgestellten Zertifikat die Zertifizierungsstelle enthält. Die URLs, die in diesem Abschnittder CAPolicy.inf-Datei angegeben sind in das Zertifikat der Stammzertifizierungsstelle selbst enthalten.

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

Einige zusätzliche Informationen zu diesem Abschnitt:

-   Mehrere URLs werden unterstützt.

-   HTTP, FTP und LDAP-URLs werden unterstützt. HTTPS-URLs werden nicht unterstützt.

-   In diesem Abschnittwird nur verwendet, wenn Sie zum Einrichten einer Stamm-ZS oder erneuern das Zertifikat der Stammzertifizierungsstelle. Untergeordnete Zertifizierungsstelle CDP-Erweiterungen werden von der Zertifizierungsstelle bestimmt, die Zertifikat der untergeordneten Zertifizierungsstelle ausstellt.

-   URLs mit Leerzeichen müssen in Anführungszeichen gesetzt werden.

-   Wenn keine URLs – d.h. Wenn angegeben sind die **[CRLDistributionPoint]** Abschnittin der Datei vorhanden ist, jedoch leer – die Erweiterung von Sperrlisten-Verteilungspunkt vom Stamm-CA-Zertifikat fehlt. Dies ist der vorzuziehen, bei der Einrichtung einer Stamm-ZS. Windows führt keine Zertifikatsperrüberprüfung auf ein Zertifikat einer Stammzertifizierungsstelle, also die CDP-Erweiterung ein Zertifikat einer Stammzertifizierungsstelle überflüssig.

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

Sie können die Autorität für die Informationen-Zugriffspunkte in der CAPolicy.inf für das Zertifikat der Stammzertifizierungsstelle angeben.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

Einige zusätzliche Hinweise auf die Autorität für die Informationen zugreifen:

-   Mehrere URLs werden unterstützt.

-   HTTP, FTP-, LDAP- und Datei-URLs werden unterstützt. HTTPS-URLs werden nicht unterstützt.

-   In diesem Abschnittwird nur verwendet, wenn Sie zum Einrichten einer Stamm-ZS, oder das Zertifikat der Stammzertifizierungsstelle erneuern. Untergeordnete Zertifizierungsstelle AIA-Erweiterungen werden von der Zertifizierungsstelle bestimmt, die der untergeordnete ZS-Zertifikat ausgestellt hat.

-   URLs mit Leerzeichen müssen in Anführungszeichen gesetzt werden.

-   Wenn keine URLs – d.h. Wenn angegeben sind die **[AuthorityInformationAccess]** Abschnittin der Datei vorhanden ist, jedoch leer – die Erweiterung von Sperrlisten-Verteilungspunkt vom Stamm-CA-Zertifikat fehlt. In diesem Fall wäre dies die bevorzugte Einstellung im Falle einer Stamm-Zertifizierungsstellenzertifikat vorhanden ist keine Autorität höher als Stamm-ZS, die durch einen Link zu das Zertifikat verwiesen werden muss.

### <a name="certsrvserver"></a>certsrv_Server

Die CAPolicy.inf kann optionaler den Abschnitt [Certsrv_server], ist die wird verwendet, um die Schlüssellänge erneuert werden kann, die Gültigkeitsdauer erneuert werden kann und die Gültigkeitszeitraum der Zertifikatsperrliste (CRL) für eine Zertifizierungsstelle angeben, ist erneuert oder installiert wird. Keine der entsprechenden Tasten in diesem Abschnittsind erforderlich. Viele dieser Einstellungen verfügen über Standardwerte, die für die meisten Anforderungen ausreichend und können einfach aus der Datei CAPolicy.inf weggelassen werden. Alternativ können viele dieser Einstellungen geändert werden, nach der Installation der Zertifizierungsstelle.

Ein Beispiel aussehen würde:

```
[certsrv_server]
RenewalKeyLength=2048
RenewalValidityPeriod=Years
RenewalValidityPeriodUnits=5
CRLPeriod=Days
CRLPeriodUnits=2
CRLDeltaPeriod=Hours
CRLDeltaPeriodUnits=4
ClockSkewMinutes=20
LoadDefaultTemplates=True
AlternateSignatureAlgorithm=0
ForceUTF8=0
EnableKeyCounting=0
```

**RenewalKeyLength** legt die Größe des Schlüssels für die Erneuerung. Dies wird nur verwendet, wenn ein neues Schlüsselpaar, während der Erneuerung eines Zertifikats generiert wird. Die Größe des Schlüssels für das anfängliche Zertifizierungsstellenzertifikat wird festgelegt, wenn die Zertifizierungsstelle installiert ist.

Wenn ein Zertifikat mit einem neuen Schlüsselpaar zu erneuern, kann die Länge des Schlüssels entweder vergrößert oder verkleinert werden. Wenn Sie einen Stamm-CA-Schlüssellänge von 4096 Byte oder höher festgelegt haben, und klicken Sie dann zu, die ermitteln müssen Sie z.B. Java-Apps oder Netzwerkgeräte, die nur Schlüsselgrößen 2048 Bytes unterstützen können. Ob Sie vergrößern oder verkleinern, müssen Sie alle von dieser Zertifizierungsstelle ausgestellten Zertifikate neu ausstellen.

**RenewalValidityPeriod** und **RenewalValidityPeriodUnits** die Lebensdauer des neuen Stamm-ZS-Zertifikats herstellen, wenn das alte Stamm-CA-Zertifikat zu erneuern. Es gilt nur für eine Stammzertifizierungsstelle. Die Gültigkeitsdauer des Zertifikats von einer untergeordneten Zertifizierungsstelle wird von dem übergeordneten bestimmt. RenewalValidityPeriod kann die folgenden Werte haben: Stunden, Tage, Wochen, Monate und Jahre.

**"CRLPeriod"** und **CRLPeriodUnits** legen Sie die Gültigkeitsdauer für die Basissperrliste. **"CRLPeriod"** können die folgenden Werte haben: Stunden, Tage, Wochen, Monate und Jahre.

**CRLDeltaPeriod** und **CRLDeltaPeriodUnits** die Gültigkeitsdauer der Deltasperrliste. **CRLDeltaPeriod** können die folgenden Werte haben: Stunden, Tage, Wochen, Monate und Jahre.

Jede dieser Einstellungen kann konfiguriert werden, nach der Installation der Zertifizierungsstelle:

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

Denken Sie daran, Active Directory-Zertifikatdienste für die Änderungen wirksam werden neu zu starten.

**LoadDefaultTemplates** gilt nur während der Installation einer Unternehmenszertifizierungsstelle. Diese Einstellung entweder "true" oder "false" (oder 1 oder 0), schreibt vor, wenn die Zertifizierungsstelle mit einem der Standardvorlagen konfiguriert ist.

In einer Standardinstallation von der Zertifizierungsstelle wird eine Teilmenge der Standardzertifikatvorlagen in den Ordner "Zertifikatvorlagen" in der Zertifizierungsstellen-Snap-In hinzugefügt. Dies bedeutet, dass, sobald der AD CS-Dienst gestartet wird, nach der Installation der Rolle eines Benutzers oder Computers mit ausreichenden Berechtigungen sofort für ein Zertifikat registrieren kann.

Sie möchten möglicherweise keine Zertifikate ausstellen sofort nach eine Zertifizierungsstelle installiert wurde, damit Sie die Einstellung LoadDefaultTemplates verwenden können, um zu verhindern, dass die Standardvorlagen Unternehmenszertifizierungsstelle hinzugefügt wird. Wenn keine Vorlagen, die auf der Zertifizierungsstelle konfiguriert sind, kann es keine Zertifikate ausstellen.

**AlternateSignatureAlgorithm** konfiguriert die Zertifizierungsstelle, um das Format der PKCS\ 1 v2. 1-Signatur für das Zertifizierungsstellenzertifikat und die Zertifikatanforderungen zu unterstützen. Bei Festlegung auf 1 in einer Stammzertifizierungsstelle wird Zertifizierungsstelle das Zertifikat der Zertifizierungsstelle das Format der PKCS\ 1 v2. 1-Signatur enthalten. Bei Festlegung auf eine untergeordnete Zertifizierungsstelle, die untergeordnete Zertifizierungsstelle eine Zertifikatanforderung erstellt, enthält das PKCS\ 1 v2. 1-Signatur-Format.

**ForceUTF8** ändert die Standard-Codierung RDNs (RDNs) im Betreff und Aussteller definierte Namen in UTF-8. Nur diese RDNs, die UTF-8, z.B. zu unterstützen, die als Directory Zeichenfolgentypen durch eine RFC betroffen sind definiert sind. Beispielsweise unterstützt den definierten Namen für die Domäne-Komponente (DC) während der Country RDN (C) unterstützt nur die Codierung als druckbare Zeichenfolge als IA5 oder UTF-8-Codierung. Die Richtlinie ForceUTF8 wirkt sich daher ein DC definierten Namen jedoch wirkt sich nicht auf eine C definierten Namen.

**EnableKeyCounting** konfiguriert die Zertifizierungsstelle, um einen Zähler zu erhöhen, jedes Mal, wenn die Zertifizierungsstelle Signaturschlüssel verwendet wird. Aktivieren Sie diese Einstellung nicht, es sei denn, Sie haben ein Hardwaresicherheitsmodul (HSM) und die zugehörigen Kryptografiedienstanbieter (CSP), die wichtigsten zählen unterstützt. Microsoft starker CSP weder die Schlüssel zählen Microsoft Software Schlüsselspeicheranbieter (KSP) unterstützt.


## <a name="create-the-capolicyinf-file"></a>Erstellen Sie die CAPolicy.inf-Datei

Vor der Installation von AD CS konfigurieren Sie die CAPolicy.inf-Datei mit spezifischen Einstellungen für die Bereitstellung.

**Voraussetzung:** müssen Sie Mitglied der Gruppe "Administratoren" sein.

1.  Geben Sie auf dem Computer, in dem Sie planen, installieren AD CS, öffnen Sie Windows PowerShell, **Editor C:.inf** und drücken Sie die EINGABETASTE.

2.  Wenn Sie dazu aufgefordert werden, um eine neue Datei zu erstellen, klicken Sie auf **Ja **.

3.  Geben Sie den folgenden als Inhalt der Datei:
   ```
   [Version]  
    Signature="$Windows NT$"  
    [PolicyStatementExtension]  
    Policies=InternalPolicy  
    [InternalPolicy]  
    OID=1.2.3.4.1455.67.89.5  
    Notice="Legal Policy Statement"  
    URL=http://pki.corp.contoso.com/pki/cps.txt  
    [Certsrv_Server]  
    RenewalKeyLength=2048  
    RenewalValidityPeriod=Years  
    RenewalValidityPeriodUnits=5  
    CRLPeriod=weeks  
    CRLPeriodUnits=1  
    LoadDefaultTemplates=0  
    AlternateSignatureAlgorithm=1  
    [CRLDistributionPoint]  
    [AuthorityInformationAccess]
   ```
1.  Klicken Sie auf **Datei**, und klicken Sie dann auf **speichern unter **.

2.  Navigieren Sie zum Ordner "% SystemRoot%".

3.  Stellen Sie Folgendes sicher:

    -   **Dateiname** läuft **Datei "CAPolicy.inf"**

    -   **Dateityp** läuft **alle Dateien**

    -   **Codierung** ist **ANSI**

4.  Klicken Sie auf **speichern**.

5.  Wenn Sie aufgefordert werden, die Datei zu überschreiben, klicken Sie auf **Ja**.

    ![Speichern Sie als Speicherort für die CAPolicy.inf-Datei](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

    >   [!CAUTION]  
    >   Achten Sie darauf, dass die CAPolicy.inf mit der Erweiterung INF-Datei zu speichern. Wenn Sie nicht speziell eingeben **inf** am Ende der Dateiname und die beschriebenen Optionen auswählen, die Datei als Textdatei gespeichert und nicht während der Zertifizierungsstelleninstallation verwendet.

6.  Schließen Sie Editor.

>   [!IMPORTANT]  
>   In der CAPolicy.inf, können Sie sehen, ist eine Linie, die URL des http://pki.corp.contoso.com/pki/cps.txt. Abschnittinternen Richtlinien die CAPolicy.inf wird nur angezeigt, als Beispiel dafür, wie Sie den Speicherort der ein Zertifikat Practice Statement (CPS) angeben möchten. In diesem Handbuch werden Sie nicht angewiesen, um die Certificate Practice-Anweisung (CPS) zu erstellen.
