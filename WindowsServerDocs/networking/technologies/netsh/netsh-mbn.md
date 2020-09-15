---
title: Netsh-Befehle für das mobile Breitbandnetzwerk (MBN)
description: Verwendet „netsh mbn“, um Einstellungen und Parameter für mobiles Breitband abzufragen und zu konfigurieren.
ms.topic: article
author: apdutta
ms.author: apdutta
ms.date: 02/20/2020
ms.openlocfilehash: 30d81f8c36c5ba745d0af1d940d8f4f3971d37a0
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078567"
---
# <a name="netsh-mbn-commands"></a>„netsh mbn“-Befehle


Verwendet **netsh mbn**, um Einstellungen und Parameter für mobiles Breitband abzufragen und zu konfigurieren.

> [!TIP]
> Hilfe zum Befehl „netsh mbn“ erhalten Sie,durch Verwenden von
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh mbn /?

Die verfügbaren „netsh mbn“-Befehle sind:

- [add](#add)
- [connect](#connect)
- [delete](#delete)
- [disconnect](#disconnect)
- [diagnose](#diagnose)
- [dump](#dump)
- [help](#help)
- [set](#set)
- [show](#show)

## <a name="add"></a>hinzufügen

Fügt einen Konfigurationseintrag zu einer Tabelle hinzu.

Die verfügbaren „netsh mbn add“-Befehle sind:

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

Fügt ein DM-Konfigurationsprofil in den Profildatenspeicher ein.

**Syntax**

```powershell
add dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Name der Profil-XML-Datei. Dabei handelt es sich um den Namen der XML-Datei, die die Profildaten enthält.     | Erforderlich |


**Beispiel**

```powershell
add dmprofile interface="Cellular" name="Profile1.xml"
```


### <a name="profile"></a>Profil

Fügt ein Netzwerkprofil in den Profildatenspeicher ein.

**Syntax**

```powershell
add profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Name der Profil-XML-Datei. Dabei handelt es sich um den Namen der XML-Datei, die die Profildaten enthält.     | Erforderlich |


**Beispiel**

```powershell
add profile interface="Cellular" name="Profile1.xml"
```


## <a name="connect"></a>connect

Stellt eine Verbindung mit einem mobilen Breitbandnetzwerk her.

**Syntax**

```powershell
connect [interface=]<string> [connmode=]tmp|name [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **connmode**  | Gibt an, wie Verbindungsparameter bereitgestellt werden. Die Verbindung kann mithilfe einer Profil-XML oder mithilfe des Profilnamens für die Profil-XML angefordert werden, die zuvor im Profildatenspeicher für mobiles Breitband mit dem Befehl „netsh mbn add profile“ gespeichert wurde. Im ersten Fall muss der Parameter „connmode“ den Wert „tmp“ enthalten. Im letzteren Fall hingegen muss der Wert „name“ lauten.                                       | Erforderlich |
| **name**      | Name der Profil-XML-Datei. Dabei handelt es sich um den Namen der XML-Datei, die die Profildaten enthält.     | Erforderlich |


**Beispiele**

```powershell
connect interface="Cellular" connmode=tmp name=d:\profile.xml
connect interface="Cellular" connmode=name name=MyProfileName
```


## <a name="delete"></a>löschen

Löscht einen Konfigurationseintrag aus einer Tabelle.

Die verfügbaren „netsh mbn delete“-Befehle sind:

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

Löscht ein DM-Konfigurationsprofil aus dem Profildatenspeicher.

**Syntax**

```powershell
delete dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Name der Profil-XML-Datei. Dabei handelt es sich um den Namen der XML-Datei, die die Profildaten enthält.     | Erforderlich |

**Beispiel**

```powershell
delete dmprofile interface="Cellular" name="myProfileName"
```

### <a name="profile"></a>Profil

Löscht ein Netzwerkprofil aus dem Profildatenspeicher.

**Syntax**

```powershell
delete profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Name der Profil-XML-Datei. Dabei handelt es sich um den Namen der XML-Datei, die die Profildaten enthält.     | Erforderlich |


**Beispiel**

```powershell
delete profile interface="Cellular" name="myProfileName"
```

## <a name="diagnose"></a>diagnose

Führt Diagnosen für grundlegende Mobilfunkprobleme aus.

**Syntax**

```powershell
diagnose [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
diagnose interface="Cellular"
```


## <a name="disconnect"></a>Trennen der Verbindung

Trennt eine Verbindung mit einem mobilen Breitbandnetzwerk.

**Syntax**

```powershell
disconnect [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
disconnect interface="Cellular"
```


## <a name="dump"></a>dump

Zeigt ein Konfigurationsskript an.

Erstellt ein Skript, das die aktuelle Konfiguration enthält.  Wird dieses Skript in einer Datei gespeichert, kann es verwendet werden, um geänderte Konfigurationseinstellungen wiederherzustellen.

**Syntax**

```powershell
dump
```

## <a name="help"></a>Hilfe

Zeigt eine Liste mit Befehlen an.

**Syntax**

```powershell
help
```

## <a name="set"></a>set

Legt Konfigurationsinformationen fest.

Die verfügbaren „netsh mbn set“-Befehle sind:

- [acstate](#acstate)
- [dataenablement](#dataenablement)
- [dataroamcontrol](#dataroamcontrol)
- [enterpriseapnparams](#enterpriseapnparams)
- [highestconncategory](#highestconncategory)
- [powerstate](#powerstate)
- [profileparameter](#profileparameter)
- [slotmapping](#slotmapping)
- [tracing](#tracing)

### <a name="acstate"></a>acstate

Legt den automatischen Verbindungsstatus für mobile Breitbanddaten für die angegebene Schnittstelle fest.

**Syntax**

```powershell
set acstate [interface=]<string> [state=]autooff|autoon|manualoff|manualon
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Der festzulegende automatische Verbindungsstatus. Einer der folgenden Werte:<br>autooff: Automatisches Verbindungstoken aus.<br>autoon: Automatisches Verbindungstoken ein.<br>manualoff: Manuelles Verbindungstoken aus.<br>manualon: Manuelles Verbindungstoken ein. | Erforderlich |


**Beispiel**

```powershell
set acstate interface="Cellular" state=autoon
```


### <a name="dataenablement"></a>dataenablement

Schaltet die mobilen Breitbanddaten für den angegebenen Profilsatz und die angegebene Schnittstelle ein bzw. aus.

**Syntax**

```powershell
set dataenablement [interface=]<string> [profileset=]internet|mms|all [mode=]yes|no
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **profileset** | Name des Profilsatzes.                                                                      | Erforderlich |
| **mode**       | Einer der folgenden Werte:<br>yes: Aktiviert den Zielprofilsatz.<br>no: Deaktiviert den Zielprofilsatz.| Erforderlich |


**Beispiel**

```powershell
set dataenablement interface="Cellular" profileset=mms mode=yes
```


### <a name="dataroamcontrol"></a>dataroamcontrol

Legt den Roamingsteuerelement-Status für mobile Breitbanddaten für den angegebenen Profilsatz und die angegebene Schnittstelle fest.

**Syntax**

```powershell
set dataroamcontrol [interface=]<string> [profileset=]internet|mms|all [state=]none|partner|all
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **profileset** | Name des Profilsatzes.                                                                      | Erforderlich |
| **mode**       | Einer der folgenden Werte:<br>none: Nur Heimnetzbetreiber.<br>partner: Nur Heim- und Partnernetzbetreiber.<br>all: Heim-, Partner- und Roamingnetzbetreiber.| Erforderlich |


**Beispiel**

```powershell
set dataroamcontrol interface="Cellular" profileset=mms mode=partner
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

Legt die enterpriseAPN-Parameter für mobile Breitbanddaten für die angegebene Schnittstelle fest.

**Syntax**

```powershell
set enterpriseapnparams [interface=]<string> [allowusercontrol=]yes|no|nc [allowuserview=]yes|no|nc [profileaction=]add|delete|modify|nc
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **allowusercontrol** | Einer der folgenden Werte:<br>yes: enterpriseAPN für das Endbenutzer-Steuerelement zulassen.<br>no: enterpriseAPN für das Endbenutzer-Steuerelement nicht zulassen.<br>nc: keine Änderung. | Erforderlich |
| **allowuserview** |Einer der folgenden Werte:<br>yes: enterpriseAPN für die Endbenutzeransicht zulassen.<br>no: enterpriseAPN für die Endbenutzeransicht nicht zulassen.<br>nc: keine Änderung. | Erforderlich |
| **profileaction** | Einer der folgenden Werte:<br>add: Ein enterpriseAPN-Profil wurde soeben hinzugefügt.<br>delete: Ein enterpriseAPN-Profil wurde soeben gelöscht.<br>modify: Ein enterpriseAPN-Profil wurde soeben geändert.<br>nc: keine Änderung. | Erforderlich |


**Beispiel**

```powershell
set enterpriseapnparams interface="Cellular" profileset=mms mode=yes
```


### <a name="highestconncategory"></a>highestconncategory

Legt die höchste Verbindungskategorie für mobile Breitbanddaten für die angegebene Schnittstelle fest.

**Syntax**

```powershell
set highestconncategory [interface=]<string> [highestcc=]admim|user|operator|device
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **highestcc** | Einer der folgenden Werte:<br>admin: vom Administrator bereitgestellte Profile.<br>user: vom Benutzer bereitgestellte Profile.<br>operator: vom Operator bereitgestellte Profile.<br>device: vom Gerät bereitgestellte Profile. | Erforderlich |


**Beispiel**

```powershell
set highestconncategory interface="Cellular" highestcc=operator
```


### <a name="powerstate"></a>powerstate

Schaltet den mobilen Breitbandfunk für die angegebene Schnittstelle ein bzw. aus.

**Syntax**

```powershell
set powerstate [interface=]<string> [state=]on|off
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **state**      | Einer der folgenden Werte:<br>on: Funkgerät einschalten.<br>off: Funkgerät ausschalten. | Erforderlich |


**Beispiel**

```powershell
set powerstate interface="Cellular" state=on
```


### <a name="profileparameter"></a>profileparameter

Legt Parameter in einem mobilen Breitbandnetzwerk-Profil fest.

**Syntax**

```powershell
set profileparameter [name=]<string> [[interface=]<string>] [[cost]=default|unrestricted|fixed|variable]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Name des zu ändernden Profils. Wenn die Schnittstelle angegeben wird, wird nur das Profil auf dieser Schnittstelle geändert. | Erforderlich |
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Optional |
| **cost**      | Kosten im Zusammenhang mit dem Profil.                                                             | Optional |


**Anmerkungen**

Mindestens ein Parameter zwischen dem Schnittstellennamen und den Kosten muss angegeben werden.


**Beispiel**

```powershell
set profileparameter name="profile 1" cost=default
```


### <a name="slotmapping"></a>slotmapping

Legt die Modemsteckplatz-Zuordnung für mobiles Breitband für die angegebene Schnittstelle fest.

**Syntax**

```powershell
set slotmapping [interface=]<string> [slotindex=]<integer>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **slotindex** | Festzulegender Steckplatzindex.                                                                         | Erforderlich |


**Beispiel**

```powershell
set slotmapping interface="Cellular" slotindex=1
```


### <a name="tracing"></a>tracing

Ablaufverfolgung aktivieren oder deaktivieren.

**Syntax**

```powershell
set tracing [mode=]yes|no
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **mode**      | Einer der folgenden Werte:<br>yes: Aktiviert die Ablaufverfolgung für mobiles Breitband.<br>no: Deaktiviert die Ablaufverfolgung für mobiles Breitband.     | Erforderlich |


**Beispiel**

```powershell
set tracing mode=yes
```

## <a name="show"></a>show

Zeigt Informationen zum mobilen Breitbandnetzwerk an.

Die verfügbaren „netsh mbn set“-Befehle sind:

- [Netsh MBN-Befehle](#netsh-mbn-commands)
  - [add](#add)
    - [dmprofile](#dmprofile)
    - [profile](#profile)
  - [connect](#connect)
  - [delete](#delete)
    - [dmprofile](#dmprofile-1)
    - [profile](#profile-1)
  - [diagnose](#diagnose)
  - [disconnect](#disconnect)
  - [dump](#dump)
  - [help](#help)
  - [set](#set)
    - [acstate](#acstate)
    - [dataenablement](#dataenablement)
    - [dataroamcontrol](#dataroamcontrol)
    - [enterpriseapnparams](#enterpriseapnparams)
    - [highestconncategory](#highestconncategory)
    - [powerstate](#powerstate)
    - [profileparameter](#profileparameter)
    - [slotmapping](#slotmapping)
    - [tracing](#tracing)
  - [show](#show)
    - [acstate](#acstate-1)
    - [capability](#capability)
    - [connection](#connection)
    - [dataenablement](#dataenablement-1)
    - [dataroamcontrol](#dataroamcontrol-1)
    - [dmprofiles](#dmprofiles)
    - [enterpriseapnparams](#enterpriseapnparams-1)
    - [highestconncategory](#highestconncategory-1)
    - [homeprovider](#homeprovider)
    - [interfaces](#interfaces)
    - [netlteattachinfo](#netlteattachinfo)
    - [pin](#pin)
    - [pinlist](#pinlist)
    - [preferredproviders](#preferredproviders)
    - [profiles](#profiles)
    - [profilestate](#profilestate)
    - [provisionedcontexts](#provisionedcontexts)
    - [purpose](#purpose)
    - [radio](#radio)
    - [readyinfo](#readyinfo)
    - [signal](#signal)
    - [slotmapping](#slotmapping-1)
    - [slotstatus](#slotstatus)
    - [smsconfig](#smsconfig)
    - [tracing](#tracing-1)
    - [visibleproviders](#visibleproviders)

### <a name="acstate"></a>acstate

Zeigt den automatischen Verbindungsstatus für mobile Breitbanddaten für die angegebene Schnittstelle an.

**Syntax**

```powershell
show acstate [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show acstate interface="Cellular"
```


### <a name="capability"></a>capability

Zeigt Informationen zu den Schnittstellenfunktionen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show capability [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show capability interface="Cellular"
```


### <a name="connection"></a>connection

Zeigt die aktuellen Verbindungsinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show connection [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show connection interface="Cellular"
```


### <a name="dataenablement"></a>dataenablement

Zeigt den Aktivierungsstatus für mobile Breitbanddaten für die angegebene Schnittstelle an.

**Syntax**

```powershell
show dataenablement [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show dataenablement interface="Cellular"
```


### <a name="dataroamcontrol"></a>dataroamcontrol

Zeigt den Roamingsteuerelement-Status für mobile Breitbanddaten für die angegebene Schnittstelle an.

**Syntax**

```powershell
show dataroamcontrol [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show dataroamcontrol interface="Cellular"
```


### <a name="dmprofiles"></a>dmprofiles

Zeigt eine Liste der auf dem System konfigurierten DM-Konfigurationsprofile an.

**Syntax**

```powershell
show dmprofiles [[name=]<string>] [[interface=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Namen des anzuzeigenden Profils.                                                               | Optional |
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Optional |

**Anmerkungen**

Zeigt die Profildaten an oder listet die Profile auf dem System auf.

Wird ein Profilname angegeben, wird der Inhalt des Profils angezeigt. Andernfalls werden Profile für die Schnittstelle aufgelistet.

Wird ein Schnittstellenname angegeben, wird nur das angegebene Profil auf der angegebenen Schnittstelle aufgelistet. Andernfalls wird das erste übereinstimmende Profil angezeigt.

**Beispiel**

```powershell
show dmprofiles name="profile 1" interface="Cellular"
show dmprofiles name="profile 2"
show dmprofiles
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

Zeigt die enterpriseAPN-Parameter für mobile Breitbanddaten für die angegebene Schnittstelle an.

**Syntax**

```powershell
show enterpriseapnparams [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show enterpriseapnparams interface="Cellular"
```


### <a name="highestconncategory"></a>highestconncategory

Zeigt die höchste Verbindungskategorie für mobile Breitbanddaten für die angegebene Schnittstelle an.

**Syntax**

```powershell
show highestconncategory [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show highestconncategory interface="Cellular"
```


### <a name="homeprovider"></a>homeprovider

Zeigt die Heimanbieterinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show homeprovider [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show homeprovider interface="Cellular"
```


### <a name="interfaces"></a>interfaces

Zeigt eine Liste der mobilen Breitbandschnittstellen auf dem System an. Für diesen Befehl gebt es keine Parameter.

**Syntax**

```powershell
show interfaces
```


### <a name="netlteattachinfo"></a>netlteattachinfo

Zeigt die LTE-Attach-Informationen für das mobile Breitband für die angegebene Schnittstelle an.

**Syntax**

```powershell
show netlteattachinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show netlteattachinfo interface="Cellular"
```

### <a name="pin"></a>pin

Zeigt die PIN-Informationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show pin [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show pin interface="Cellular"
```


### <a name="pinlist"></a>pinlist

Zeigt die PIN-Listeninformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show pinlist [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show pinlist interface="Cellular"
```


### <a name="preferredproviders"></a>preferredproviders

Zeigt die Liste der bevorzugten Anbieter für die angegebene Schnittstelle an.

**Syntax**

```powershell
show preferredproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show preferredproviders interface="Cellular"
```


### <a name="profiles"></a>profiles

Zeigt eine Liste der auf dem System konfigurierten Profile an.

**Syntax**

```powershell
show profiles [[name=]<string>] [[interface=]<string>] [[purpose=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | Namen des anzuzeigenden Profils.                                                               | Optional |
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Optional |
| **purpose**   | Zweck | Optional |

**Anmerkungen**

Wird ein Profilname angegeben, wird der Inhalt des Profils angezeigt. Andernfalls werden Profile für die Schnittstelle aufgelistet.

Wird ein Schnittstellenname angegeben, wird nur das angegebene Profil auf der angegebenen Schnittstelle aufgelistet. Andernfalls wird das erste übereinstimmende Profil angezeigt.

Wird der Zweck angegeben, werden nur Profile mit der passenden Zweck-GUID angezeigt.  Andernfalls werden die Profile nicht nach dem Zweck gefiltert.  Die Zeichenfolge kann entweder eine GUID mit geschweiften Klammern oder eine der folgenden Zeichenfolgen sein: „internet“, „supl“, „mms“, „ims“ oder „allhost“.

**Beispiel**

```powershell
show profiles interface="Cellular" purpose="{00000000-0000-0000-0000-000000000000}"
show profiles name="profile 1" interface="Cellular"
show profiles name="profile 2"
show profiles
```

### <a name="profilestate"></a>profilestate

Zeigt den Status eines mobilen Breitbandprofils für die angegebene Schnittstelle an.

**Syntax**

```powershell
show profilestate [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |
| **name**      | Name des Profils. Es ist der Name des Profils, dessen Status angezeigt werden soll.            | Erforderlich |

**Beispiel**

```powershell
show profilestate interface="Cellular" name="myProfileName"
```

### <a name="provisionedcontexts"></a>provisionedcontexts

Zeigt die bereitgestellten Kontextinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show provisionedcontexts [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show provisionedcontexts interface="Cellular"
```


### <a name="purpose"></a>purpose

Zeigt die Zweckgruppen-GUIDs an, die zum Filtern von Profilen auf dem Gerät verwendet werden können. Für diesen Befehl gebt es keine Parameter.

**Syntax**

```powershell
show purpose
```


### <a name="radio"></a>radio

Zeigt die Funkzustandsinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show radio [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show radio interface="Cellular"
```


### <a name="readyinfo"></a>readyinfo

Zeigt die Informationen zur Bereitschaft für die angegebene Schnittstelle an.

**Syntax**

```powershell
show readyinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show readyinfo interface="Cellular"
```


### <a name="signal"></a>signal

Zeigt die Signalinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show signal [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show signal interface="Cellular"
```


### <a name="slotmapping"></a>slotmapping

Zeigt die Modemsteckplatz-Zuordnung für mobiles Breitband für die angegebene Schnittstelle an.

**Syntax**

```powershell
show slotmapping [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show slotmapping interface="Cellular"
```


### <a name="slotstatus"></a>slotstatus

Zeigt den Modemsteckplatz-Status für mobiles Breitband für die angegebene Schnittstelle an.

**Syntax**

```powershell
show slotstatus [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show slotstatus interface="Cellular"
```


### <a name="smsconfig"></a>smsconfig

Zeigt die SMS-Konfigurationsinformationen für die angegebene Schnittstelle an.

**Syntax**

```powershell
show smsconfig [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show smsconfig interface="Cellular"
```


### <a name="tracing"></a>tracing

Zeigt an, ob die Ablaufverfolgung für mobiles Breitband aktiviert oder deaktiviert ist.

**Syntax**

```powershell
show tracing
```


### <a name="visibleproviders"></a>visibleproviders

Zeigt die Liste der sichtbaren Anbieter für die angegebene Schnittstelle an.

**Syntax**

```powershell
show visibleproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | Schnittstellenname. Dies ist einer der durch den Befehl „netsh mbn show interfaces“ angezeigten Schnittstellennamen. | Erforderlich |


**Beispiel**

```powershell
show visibleproviders interface="Cellular"
```
