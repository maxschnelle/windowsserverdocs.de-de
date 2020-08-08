---
title: Verwenden von ETW zur Problembehandlung bei LDAP-Verbindungen
description: Informationen zum Aktivieren und Verwenden von etw für die Ablauf Verfolgung von LDAP-Verbindungen zwischen AD DS Domänen Controllern.
author: Teresa-Motiv
manager: dcscontentpm-dev
audience: Admin
ms.author: v-tea
ms.topic: article
ms.date: 11/22/2019
ms.openlocfilehash: 37f588be3b181aea66555389c120f147a74e6314
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941554"
---
# <a name="using-etw-to-troubleshoot-ldap-connections"></a>Verwenden von ETW zur Problembehandlung bei LDAP-Verbindungen

Die [Ereignis Ablauf Verfolgung für Windows (Event Tracing for Windows, etw)](/windows/win32/etw/event-tracing-portal) kann ein nützliches Problem Behandlungs Tool für Active Directory Domain Services (AD DS) sein. Sie können etw verwenden, um die[LDAP](/previous-versions/windows/desktop/ldap/lightweight-directory-access-protocol-ldap-api)-Kommunikation (Lightweight Directory Access Protocol) zwischen Windows-Clients und LDAP-Servern, einschließlich AD DS Domänen Controllern, zu verfolgen.

## <a name="how-to-turn-on-etw-and-start-a-trace"></a>Aktivieren von etw und Starten einer Ablauf Verfolgung

**So aktivieren Sie etw**

1. Öffnen Sie den Registrierungs-Editor, und erstellen Sie den folgenden Registrierungs Unterschlüssel:

   **HKEY \_ local \_ Machine \\ System \\ CurrentControlSet \\ Services \\ LDAP \\ Tracing \\ * ProcessName***

   In diesem Unterschlüssel ist *ProcessName* der vollständige Name des Prozesses, den Sie verfolgen möchten, einschließlich der Erweiterung (z. b. "Svchost.exe").

1. (**Optional**) Erstellen Sie unter diesem Unterschlüssel einen neuen Eintrag mit dem Namen **PID**. Wenn Sie diesen Eintrag verwenden möchten, weisen Sie eine Prozess-ID als DWORD-Wert zu.

   Wenn Sie eine Prozess-ID angeben, verfolgt etw nur die Instanz der Anwendung, die diese Prozess-ID aufweist.

**So starten Sie eine Ablauf Verfolgungs Sitzung**

- Öffnen Sie ein Eingabe Aufforderungs Fenster, und führen Sie den folgenden Befehl aus:

   ```cmd
   tracelog.exe -start <SessionName> -guid \#099614a5-5dd7-4788-8bc9-e29f43db28fc -f <FileName> -flag <TraceFlags>
   ```

   Die Platzhalter in diesem Befehl stellen die folgenden Werte dar.

  - \<*SessionName*>ist ein beliebiger Bezeichner, der zum bezeichnen der Ablauf Verfolgungs Sitzung verwendet wird.
  > [!NOTE]
  > Wenn Sie die Ablauf Verfolgungs Sitzung beenden, müssen Sie später auf diesen Sitzungs Namen verweisen.
  - \<*FileName*>Gibt die Protokolldatei an, in die Ereignisse geschrieben werden.
  - \<*TraceFlags*>muss mindestens einer der Werte sein, die in der Ablaufverfolgungsflags- [Tabelle](#values-for-trace-flags)aufgeführt sind.

## <a name="how-to-end-a-tracing-session-and-turn-off-event-tracing"></a>Beenden einer Ablauf Verfolgungs Sitzung und Deaktivieren der Ereignis Ablauf Verfolgung

**So stoppt die Ablauf Verfolgung**

- Führen Sie an der Eingabeaufforderung den folgenden Befehl aus:

   ```cmd
   tracelog.exe -stop <SessionName>
   ```

   In diesem Befehl \<*SessionName*> ist derselbe Name, den Sie im **tracelog.exe-Start-** Befehl verwendet haben.

**So deaktivieren Sie etw**

- Löschen Sie im Registrierungs-Editor den Unterschlüssel **HKEY \_ local \_ Machine \\ System \\ CurrentControlSet \\ Services \\ LDAP \\ Tracing \\ * ProcessName***.

## <a name="values-for-trace-flags"></a>Werte für Ablaufverfolgungsflags

Um ein Flag zu verwenden, ersetzen Sie den-Flag-Wert für den <*TraceFlags*> Platzhalter in den Argumenten des **tracelog.exe-Start-** Befehls.

> [!NOTE]
> Sie können mehrere Flags angeben, indem Sie die Summe der entsprechenden Flagwerte verwenden. Um z. b. die Flags für die **Debug- \_ Suche** (0x00000001) und den **Debug- \_ Cache** (0x00000010) anzugeben, ist der entsprechende \<*TraceFlags*> Wert **0x00000011**.

|Flagname |Flagwert |Flag-Beschreibung |
| --- | --- | --- |
|**DEBUG_SEARCH** |0x00000001 |Protokolliert Suchanforderungen und die Parameter, die an diese Anforderungen übermittelt werden. Antworten werden hier nicht protokolliert. Nur die Suchanforderungen werden protokolliert. (Verwenden Sie **DEBUG_SPEWSEARCH** , um die Antworten auf Suchanforderungen zu protokollieren.) |
|**DEBUG_WRITE** |0x00000002 |Protokolliert Schreib Anforderungen und die Parameter, die an diese Anforderungen übermittelt werden. Zu den Schreib Anforderungen gehören die Add-, DELETE-, Modify-und Extended-Vorgänge. |
|**DEBUG_REFCNT** |0x00000004 |Protokolliert Verweis zählungs Daten und Vorgänge für Verbindungen und Anforderungen. |
|**DEBUG_HEAP** |0x00000008 |Protokolliert alle Speicher Belegungen und Speicher Releases. |
|**DEBUG_CACHE** |0x00000010 |Protokolliert Cache Aktivitäten. Diese Aktivität schließt Hinzufügungen, Entfernens, Treffer, Fehler usw. ein. |
|**DEBUG_SSL** |0x00000020 |Protokolliert SSL-Informationen und-Fehler. |
|**DEBUG_SPEWSEARCH** |0x00000040 |Protokolliert alle Server Antworten auf Suchanforderungen. Diese Antworten beinhalten die angeforderten Attribute sowie alle empfangenen Daten. |
|**DEBUG_SERVERDOWN** |0x00000080 |Protokolliert Server-Down-und Verbindungsfehler. |
|**DEBUG_CONNECT** |0x00000100 |Protokolliert Daten im Zusammenhang mit dem Herstellen einer Verbindung.<br />Verwenden Sie **DEBUG_CONNECTION** , um andere Daten zu protokollieren, die sich auf Verbindungen beziehen. |
|**DEBUG_RECONNECT** |0x00000200 |Protokolliert die automatische Wiederherstellung der Verbindungs Aktivität. Diese Aktivität umfasst Verbindungsversuche, Ausfälle und zugehörige Fehler. |
|**DEBUG_RECEIVEDATA** |0x00000400 |Protokolliert Aktivitäten, die sich auf den Empfang von Nachrichten vom Server beziehen. Diese Aktivität schließt Ereignisse ein, z. b. "warten auf die Antwort vom Server" und die vom Server empfangene Antwort. |
|**DEBUG_BYTES_SENT** |0x00000800 |Protokolliert alle Daten, die vom LDAP-Client an den Server gesendet werden. Diese Funktion ist im Wesentlichen die Paket Protokollierung, protokolliert jedoch immer unverschlüsselte Daten. (Wenn ein Paket über SSL gesendet wird, protokolliert diese Funktion das unverschlüsselte Paket.) Diese Protokollierung kann ausführlich sein. Dieses Flag wird wahrscheinlich am besten oder in Kombination mit **DEBUG_BYTES_RECEIVED**verwendet. |
|**DEBUG_EOM** |0x00001000 |Protokolliert Ereignisse, die mit dem Erreichen des Endes einer Meldungs Liste verknüpft sind. Diese Ereignisse enthalten Informationen wie "Meldungs Liste gelöscht" usw. |
|**DEBUG_BER** |0x00002000 |Protokolliert Vorgänge und Fehler, die sich auf grundlegende Codierungsregeln (ber) beziehen. Zu diesen Vorgängen und Fehlern zählen Probleme bei der Codierung, Puffergrößen Probleme usw. |
|**DEBUG_OUTMEMORY** |0x00004000 |Protokolliert Fehler, um Arbeitsspeicher zuzuweisen. Protokolliert auch jeden Fehler, um den erforderlichen Arbeitsspeicher zu berechnen (z. b. einen Überlauf, der beim Berechnen der erforderlichen Puffergröße auftritt). |
|**DEBUG_CONTROLS** |0x00008000 |Protokolliert Daten, die sich auf Steuerelemente beziehen. Zu diesen Daten gehören eingefügte Steuerelemente, Probleme, die sich auf Steuerelemente auswirken, obligatorische Steuerelemente für eine Verbindung usw. |
|**DEBUG_BYTES_RECEIVED** |0x00010000 |Protokolliert alle Daten, die vom LDAP-Client empfangen werden. Dieses Verhalten ist im Wesentlichen die Paket Protokollierung, protokolliert jedoch immer unverschlüsselte Daten. (Wenn ein Paket über SSL gesendet wird, protokolliert diese Option das unverschlüsselte Paket.) Diese Art der Protokollierung kann ausführlich sein. Dieses Flag wird wahrscheinlich am besten oder in Kombination mit **DEBUG_BYTES_SENT**verwendet. |
|**DEBUG_CLDAP** |0x00020000 |Protokolliert Ereignisse, die für UDP und verbindungsloses LDAP spezifisch sind. |
|**DEBUG_FILTER** |0x00040000 |Protokolliert Ereignisse und Fehler, die beim Erstellen eines Suchfilters auftreten.<br/>**Hinweis** Mit dieser Option werden Client Ereignisse nur während der Filter Erstellung protokolliert. Es werden keine Antworten vom Server über einen Filter protokolliert. |
|**DEBUG_BIND** |0x00080000 |Protokolliert die Bindungs Ereignisse und-Fehler. Zu diesen Daten gehören Aushandlungs Informationen, der Bindungs Erfolg, der Bindungs Fehler usw. |
|**DEBUG_NETWORK_ERRORS** |0x00100000 |Protokolliert allgemeine Netzwerkfehler. Diese Daten umfassen Sende-und Empfangs Fehler.<br/>**Hinweis** Wenn eine Verbindung verloren geht oder der Server nicht erreicht werden kann, ist **DEBUG_SERVERDOWN** das bevorzugte Tag. |
|**DEBUG_VERBOSE** |0x00200000 |Protokolliert Allgemeine Meldungen. Verwenden Sie diese Option für alle Nachrichten, die tendenziell eine große Menge an Ausgabe generieren. Beispielsweise werden Meldungen wie "Ende der Nachricht erreicht", "der Server hat noch nicht geantwortet" usw. protokolliert. Diese Option ist auch bei generischen Nachrichten nützlich. |
|**DEBUG_PARSE** |0x00400000 |Protokolliert allgemeine Nachrichten Ereignisse und-Fehler sowie paketparsing-und Codierungs Ereignisse und-Fehler. |
|**DEBUG_REFERRALS** |0x00800000 |Protokolliert Daten über Verweise und Verweigerungen für Verweise. |
|**DEBUG_REQUEST** |0x01000000 |Protokolliert die Nachverfolgung von Anforderungen. |
|**DEBUG_CONNECTION** |0x02000000 |Protokolliert allgemeine Verbindungsdaten und Fehler. |
|**DEBUG_INIT_TERM** |0x04000000 |Protokolliert die Modul Initialisierung und-Bereinigung (dll-Main usw.). |
|**DEBUG_API_ERRORS** |0x08000000 |Unterstützt die Protokollierung falscher Verwendung der API. Diese Option protokolliert z. b. Daten, wenn der Bindungs Vorgang zweimal auf derselben Verbindung aufgerufen wird. |
|**DEBUG_ERRORS** |0x10000000 |Protokolliert allgemeine Fehler. Die meisten dieser Fehler können als Modul Initialisierungsfehler, SSL-Fehler oder Überlauf-oder Unterlauf Fehler kategorisiert werden. |
|**DEBUG_PERFORMANCE** |0x20000000 |Protokolliert Daten über Prozess-globale LDAP-Aktivitäts Statistiken nach dem Empfang einer Serverantwort für eine LDAP-Anforderung. |

## <a name="example"></a>Beispiel

Angenommen, eine Anwendung, App1.exe, mit der Kenn Wörter für Benutzerkonten festgelegt werden. Angenommen, App1.exe erzeugt einen unerwarteten Fehler. Führen Sie die folgenden Schritte aus, um mithilfe von etw das Problem zu diagnostizieren:

1. Erstellen Sie im Registrierungs-Editor den folgenden Registrierungs Eintrag:

   **HKEY \_ local \_ Machine \\ System \\ CurrentControlSet \\ Services \\ LDAP-Ablauf \\ Verfolgungs \\App1.exe**

1. Öffnen Sie ein Eingabe Aufforderungs Fenster, und führen Sie den folgenden Befehl aus, um eine Ablauf Verfolgungs Sitzung zu starten:

   ```cmd
   tracelog.exe -start ldaptrace -guid \#099614a5-5dd7-4788-8bc9-e29f43db28fc -f .\ldap.etl -flag 0x80000
   ```

   Nachdem dieser Befehl gestartet wurde, stellt die **Debug- \_ Bindung** sicher, dass etw Ablauf Verfolgungs Meldungen in schreibt. \\ LDAP. ETL.

1. Starten Sie App1.exe, und reproduzieren Sie den unerwarteten Fehler.

1. Um die Ablauf Verfolgungs Sitzung zu verhindern, führen Sie den folgenden Befehl an der Eingabeaufforderung aus:

   ```cmd
    tracelog.exe -stop ldaptrace
   ```

1. Um zu verhindern, dass andere Benutzer die Anwendung nachverfolgen, löschen Sie den Registrierungs Eintrag **HKEY \_ local \_ Machine** \\ **System** \\ **CurrentControlSet** \\ **Services** \\ **LDAP** \\ **Tracing** \\ **App1.exe** .

1. Um die Informationen im Ablauf Verfolgungs Protokoll zu überprüfen, führen Sie den folgenden Befehl an der Eingabeaufforderung aus:

   ```cmd
    tracerpt.exe .\ldap.etl -o -report
    ```

   > [!NOTE]
   > In diesem Befehl ist **tracerpt.exe** ein Consumer-Tool für die Ablauf [Verfolgung](https://go.microsoft.com/fwlink/p/?linkid=83876) .
