---
title: tsecimp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7488ec6-0eff-45ff-89ee-9cbe752416bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5ed2ef8b1d0238a3608dabdd165a255855a304d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440874"
---
# <a name="tsecimp"></a>tsecimp



Importiert Informationen zur Zuordnung von einer Extensible Markup Language (XML)-Datei, in der Sicherheitsdatei von TAPI-Server (Tsec.ini). Sie können mit diesem Befehl auch verwenden, um die Liste der TAPI-Anbieter anzuzeigen und die Zeilen-Geräte in Zusammenhang mit jedem von ihnen, überprüfen Sie die Struktur der XML-Datei ohne den Inhalt zu importieren und Domänenmitgliedschaft zu überprüfen.

## <a name="syntax"></a>Syntax

```
tsecimp /f <Filename> [{/v | /u}]
tsecimp /d
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ f \<Dateiname >|Erforderlich. Gibt den Namen der XML-Datei, die die Informationen zur Zuordnung enthält, die Sie importieren möchten.|
|/v|Überprüft die Struktur der XML-Datei ohne die Informationen in die Tsec.ini-Datei zu importieren.|
|/u|Überprüft, ob jeder Benutzer Mitglied der Domäne, die in der XML-Datei angegeben ist. Der Computer, auf dem Sie diesen Parameter verwenden, muss mit dem Netzwerk verbunden werden. Dieser Parameter möglicherweise Leistung stark beeinträchtigt, wenn Sie eine große Menge von Informationen zur Zuordnung verarbeitet werden.|
|/d|Zeigt eine Liste der installierten Telefonieanbieter. Für jeden Telefonieanbieter werden die dazugehörigen Linie Geräte aufgeführt, sowie die Adressen und die Benutzer und jedes Gerät Zeile zugeordnet sind.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die XML-Datei, die von der Sie die Informationen zur Zuordnung importieren möchten, muss die unten beschriebene Struktur folgen.  
    -   **UserList** Element

        Die **UserList** ist das oberste Element der XML-Datei.
    -   **Benutzer** Element

        Jede **Benutzer** Element enthält Informationen zu einem Benutzer, die einer Domäne angehört. Jeder Benutzer kann eine oder mehrere Zeile Geräten zugewiesen werden.

        Darüber hinaus jede **Benutzer** Element handelt es sich möglicherweise um ein Attribut namens **NoMerge**. Wenn dieses Attribut angegeben wird, werden alle gerätezuweisungen aktuelle Zeile für den Benutzer entfernt, bevor neue vorgenommen werden. Sie können dieses Attribut verwenden, um unerwünschte benutzerzuweisungen problemlos entfernen. Standardmäßig ist dieses Attribut nicht festgelegt.

        Die **Benutzer** -Element muss ein einzelnes enthalten **DomainUserName** Element, das die Domäne und den Namen des Benutzers angibt. Die **Benutzer** Element kann auch eine enthalten **FriendlyName** Element, das einen Anzeigenamen für den Benutzer angibt.

        Die **Benutzer** Element möglicherweise einen enthalten **LineList** Element. Wenn eine **LineList** Element ist nicht vorhanden, werden alle Zeile Geräte für diesen Benutzer entfernt werden.
    -   **LineList** Element

        Die **LineList** Element enthält Informationen über jede Zeile oder ein Gerät, das dem Benutzer zugewiesen werden kann. Jede **LineList** Element kann mehrere panele enthalten **Zeile** Element.
    -   **Zeile** Element

        Jede **Zeile** Element gibt ein Gerät für die Zeile an. Müssen Sie jedes Gerät für die Zeile identifizieren, indem Sie entweder Hinzufügen einer **Adresse** Element oder ein **PermanentID** Element unter den **Zeile** Element.

        Für jede **Zeile** -Element, Sie können festlegen, die **entfernen** Attribut. Wenn Sie dieses Attribut festlegen, erhält der Benutzer das Gerät für die Zeile nicht mehr. Wenn dieses Attribut nicht festgelegt ist, erhält der Benutzer den Zugriff auf das Gerät für die Zeile an. Wenn das Gerät nicht verfügbar, die dem Benutzer ist kein Fehler ausgegeben.

## <a name="examples"></a>Beispiele
- Das folgende Beispiel XML-Code-Segmente veranschaulichen die korrekte Verwendung der oben definierten Elemente.  
  - Der folgende Code entfernt alle "user1" zugewiesen.  
    ```
    <UserList>
      <User NoMerge="1">
        <DomainUser>domain1\user1</DomainUser>
      </User>
    </UserList>
    ```  
  - Der folgende Code entfernt alle "user1" zugewiesen sind, bevor Sie eine Zeile mit der Adresse 99999 zuweisen. "User1" müssen keine weiteren Zeilen Geräte zugewiesen, unabhängig davon, ob alle Geräte Zeile zuvor zugewiesen wurden.  
    ```
    <UserList>
      <User NoMerge="1">
        <DomainUser>domain1\user1</DomainUser>
        <FriendlyName>User1</FriendlyName>
        <LineList>
          <Line>
            <Address>99999</Address>
          </Line>
        </LineList>
      </User>
    </UserList>
    ```  
  - Der folgende Code Fügt eine Zeile Gerät für "user1" ohne alle zuvor zugewiesenen Zeile Geräte zu löschen.  
    ```
    <UserList>
      <User>
        <DomainUser>domain1\user1</DomainUser>
        <FriendlyName>User1</FriendlyName>
        <LineList>
          <Line>
            <Address>99999</Address>
          </Line>
        </LineList>
      </User>
    </UserList>
    ```  
  - Der folgende Code fügt der Zeile Adresse 99999 und Anschlussadresse 88888 "user1"s Zugriff entfernt.  
    ```
    <UserList>
      <User>
        <DomainUser>domain1\user1</DomainUser>
        <FriendlyName>User1</FriendlyName>
        <LineList>
          <Line>
            <Address>99999</Address>
          </Line>
          <Line Remove="1">
            <Address>88888</Address>
          </Line>
        </LineList>
      </User>
    </UserList>
    ```  
  - Der folgende Code fügt permanenten Medien 1000 und 88888 "user1"s Zugriff entfernt werden.  
    ```
    <UserList>
      <User>
        <DomainUser>domain1\user1</DomainUser>
        <FriendlyName>User1</FriendlyName>
        <LineList>
          <Line>
            <PermanentID>1000</PermanentID>
          </Line>
          <Line Remove="1">
            <Address>88888</Address>
          </Line>
        </LineList>
      </User>
    </UserList>


~~~
    ```  
~~~
-   The following sample output appears after the **/d** command-line option is specified to display the current TAPI configuration. For each telephony provider, the associated line devices are listed, as well as the addresses and users associated with each line device.  
    ```
    NDIS Proxy TAPI Service Provider
            Line: "WAN Miniport (L2TP)"
                    Permanent ID: 12345678910

    NDIS Proxy TAPI Service Provider
            Line: "LPT1DOMAIN1\User1"
                    Permanent ID: 12345678910

    Microsoft H.323 Telephony Service Provider
            Line: "H323 Line"
                    Permanent ID: 123456
                    Addresses:
                            BLDG1-TAPI32

    ```

#### Additional references

[Command-Line Syntax Key](command-line-syntax-key.md)

[Command shell overview](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)