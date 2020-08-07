---
title: ktpass
description: Referenz Artikel für den Befehl "ktpass", mit dem der Server Prinzipal Name für den Host oder Dienst in AD DS konfiguriert wird und eine keytab-Datei generiert wird, die den gemeinsamen geheimen Schlüssel des Diensts enthält.
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bb523d35a1bbf2d15895201855a58e96ebb7772
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887646"
---
# <a name="ktpass"></a>ktpass

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert den Server Prinzipal Namen für den Host oder Dienst in Active Directory Domain Services (AD DS) und generiert eine keytab-Datei, die den gemeinsamen geheimen Schlüssel des Diensts enthält. Die KEYTAB-Datei basiert auf der Massachusetts Institute of Technology (MIT)-Implementierung des Kerberos-Authentifizierungsprotokolls. Mit dem Befehlszeilenprogramm "ktpass" können nicht-Windows-Dienste, die die Kerberos-Authentifizierung unterstützen, die vom Kerberos-Schlüsselverteilungscenter (KDC) bereitgestellten Interoperabilitäts Funktionen verwenden.

## <a name="syntax"></a>Syntax

```
ktpass
[/out <filename>]
[/princ <principalname>]
[/mapuser <useraccount>]
[/mapop {add|set}] [{-|+}desonly] [/in <filename>]
[/pass {password|*|{-|+}rndpass}]
[/minpass]
[/maxpass]
[/crypto {DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}]
[/itercount]
[/ptype {KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}]
[/kvno <keyversionnum>]
[/answer {-|+}]
[/target]
[/rawsalt] [{-|+}dumpsalt] [{-|+}setupn] [{-|+}setpass <password>]  [/?|/h|/help]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ------------|
| /Out`<filename>` | Gibt den Namen der zu generierenden Datei "Kerberos 5. keytab" an. **Hinweis:** Dies ist die Datei ". keytab", die Sie auf einen Computer übertragen, auf dem das Windows-Betriebssystem nicht ausgeführt wird, und dann ersetzen oder Zusammenführen mit der vorhandenen Keytab-Datei, */etc/krb5.keytab*. |
| /princ `<principalname>` | Gibt den Prinzipal Namen im Formular an host/computer.contoso.com@CONTOSO.COM . **Warnung:** Bei diesem Parameter wird die Groß-/Kleinschreibung beachtet. |
| /mapuser `<useraccount>` | Ordnet den Namen des Kerberos-Prinzipals, der vom **princ** -Parameter angegeben wird, dem angegebenen Domänen Konto zu. |
| /mapop`{add|set}` | Gibt an, wie das Mapping-Attribut festgelegt wird.<ul><li>**Add** -addiert den Wert des angegebenen lokalen Benutzernamens. Dies ist die Standardeinstellung.</li><li>**Set** : legt den Wert für die reine Daten Verschlüsselungs Standard-Verschlüsselung für den angegebenen lokalen Benutzernamen fest.</li></ul> |
| `{-|+}`nicht ordnungsgemäß | Die nur-der-Verschlüsselung wird standardmäßig festgelegt.<ul><li>**+** Legt ein Konto für die reine des-Verschlüsselung fest.</li><li>**-** Gibt die Einschränkung für ein Konto für die reine des-Verschlüsselung frei. **Wichtig:** Der Standardwert von Windows wird von Windows nicht unterstützt.</li></ul> |
| /in`<filename>` | Gibt die Keytab-Datei an, die von einem Host Computer gelesen werden soll, auf dem das Windows-Betriebssystem nicht ausgeführt wird. |
| /pass`{password|*|{-|+}rndpass}` | Gibt ein Kennwort für den Prinzipal Benutzernamen an, der durch den **princ** -Parameter angegeben wird. Verwenden `*` Sie, um ein Kennwort einzugeben. |
| /minpass | Legt die minimale Länge des Zufalls Kennworts auf 15 Zeichen fest. |
| /maxpass | Legt die maximale Länge des Zufalls Kennworts auf 256 Zeichen fest. |
| /crypto`{DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}` | Gibt die Schlüssel an, die in der Schlüssel Tabellendatei-Datei generiert werden:<ul><li>**Des-CBC-CRC** -verwendet aus Kompatibilitätsgründen.</li><li>**Des-CBC-MD5** -hält die mit-Implementierung genauer an und wird aus Kompatibilitätsgründen verwendet.</li><li>**RC4-HMAC-NT** : verwendet die 128-Bit-Verschlüsselung.</li><li>**AES256-SHA1** : verwendet AES256-CTS-HMAC-SHA1-96-Verschlüsselung.</li><li>   **AES128-SHA1** : verwendet AES128-CTS-HMAC-SHA1-96-Verschlüsselung.</li><li>**Alle** -Zustände, die alle unterstützten kryptografietypen verwenden können.</li></ul><p>**Hinweis:** Da die Standardeinstellungen auf älteren mit-Versionen basieren, sollten Sie immer den- `/crypto` Parameter verwenden. |
| /itercount | Gibt die Anzahl der Iterationen an, die für die AES-Verschlüsselung verwendet wird. Der Standardwert ignoriert **itercount** für die nicht-AES-Verschlüsselung und legt die AES-Verschlüsselung auf 4.096 fest. |
| /ptype`{KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}` | Gibt den Prinzipaltyp an.<ul><li>**KRB5_NT_PRINCIPAL** : der allgemeine Prinzipaltyp (empfohlen).</li><li>**KRB5_NT_SRV_INST** : die Instanz des Benutzer Dienstanbieter</li><li>  **KRB5_NT_SRV_HST** -die Host Dienst Instanz</li></ul> |
| /kvno`<keyversionnum>` | Gibt die Versionsnummer des Schlüssels an. Der Standardwert ist 1. |
| /Answer`{-|+}` | Legt den Hintergrund Antwortmodus fest:<ul><li>**-** Antworten auf Kenn Wort Zurücksetzungen automatisch zurücksetzen, **ohne**.</li><li>**+** Antworten Zurücksetzen von Kenn Wort Eingabe Aufforderungen mit **Ja**.</li></ul> |
| /target | Legt fest, welcher Domänen Controller verwendet werden soll. Standardmäßig wird der Domänen Controller basierend auf dem Prinzipal Namen erkannt. Wenn der Domänen Controller Name nicht aufgelöst wird, werden Sie in einem Dialogfeld zur Eingabe eines gültigen Domänen Controllers aufgefordert. |
| /rawsalt | erzwingt, dass "ktpass" den rawsalt-Algorithmus beim Erzeugen des Schlüssels verwendet. Dieser Parameter ist optional. |
| `{-|+}dumpsalt` | Die Ausgabe dieses Parameters zeigt den mit Salt-Algorithmus, der verwendet wird, um den Schlüssel zu generieren. |
| `{-|+}setupn` | Legt den Benutzer Prinzipal Namen (User Principal Name, UPN) zusätzlich zum Dienst Prinzipal Namen (SPN) fest. Standardmäßig wird beide in der Keytab-Datei festgelegt. |
| `{-|+}setpass <password>` | Legt das Kennwort des Benutzers fest, wenn angegeben. Wenn rndpass verwendet wird, wird stattdessen ein zufälliges Kennwort generiert. |
| /? | Zeigt die Hilfe für diesen Befehl an. |

#### <a name="remarks"></a>Bemerkungen

- Dienste, die auf Systemen ausgeführt werden, auf denen das Windows-Betriebssystem nicht ausgeführt wird, können in AD DS mit Dienst Instanzen Konten konfiguriert werden. Dadurch kann sich jeder Kerberos-Client bei Diensten authentifizieren, auf denen das Windows-Betriebssystem nicht mithilfe von Windows-KDCs ausgeführt wird.

- Der **/princ** -Parameter wird nicht von "ktpass" ausgewertet und wie angegeben verwendet. Es wird nicht überprüft, ob der Parameter dem Wert des **userPrincipalName** -Attributs beim Erzeugen der Keytab-Datei entspricht. Die Unterscheidung nach Groß-/Kleinschreibung Unterscheidung bei Kerberos-Distributionen, die diese Keytab-Datei verwenden, treten möglicherweise Probleme auf, wenn keine genaue groß-und Kleinschreibung vorliegt , Um den korrekten **userPrincipalName** -Attribut Wert aus einer LDIFDE-Exportdatei zu überprüfen und abzurufen. Beispiel:

    ```
    ldifde /f keytab_user.ldf /d CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com /p base /l samaccountname,userprincipalname
    ````

### <a name="examples"></a>Beispiele

Wenn Sie eine Kerberos. keytab-Datei für einen Host Computer erstellen möchten, auf dem das Windows-Betriebssystem nicht ausgeführt wird, müssen Sie den Prinzipal dem Konto zuordnen und das Host Prinzipal Kennwort festlegen.

1. Verwenden Sie das Snap-in Active Directory **-Benutzer und-Computer** , um ein Benutzerkonto für einen Dienst auf einem Computer zu erstellen, auf dem das Windows-Betriebssystem nicht ausgeführt wird. Erstellen Sie z. b. ein Konto mit dem Namen *User1*.

2. Verwenden Sie den Befehl " **ktpass** ", um eine Identitäts Zuordnung für das Benutzerkonto einzurichten, indem Sie Folgendes eingeben:

    ```
    ktpass /princ host/User1.contoso.com@CONTOSO.COM /mapuser User1 /pass MyPas$w0rd /out machine.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set
    ```

    > [!NOTE]
    > Sie können nicht mehrere Dienst Instanzen demselben Benutzerkonto zuordnen.

3. Führen Sie die Datei ". keytab" mit der Datei */etc/krb5.keytab* auf einem Host Computer zusammen, auf dem das Windows-Betriebssystem nicht ausgeführt wird.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
