1. Haben Sie eine Directory Services-Administrator das Computerkonto für unseren neuen Knoten hinzufügen, der Sicherheitsgruppe, die mit allen Ihren HGS-Servern, die Berechtigungen festgelegt haben, können von diesen Servern das gMSA-Konto-Host-Überwachungsdienst verwendet wird.

2. Starten Sie den neuen Knoten um ein neues Kerberos-Ticket zu erhalten, das der Computer die Mitgliedschaft in dieser Sicherheitsgruppe enthält neu. Wenn der Neustart abgeschlossen ist, melden Sie sich eine Domänenidentität, zu der der lokalen Administratorengruppe auf dem Computer gehört.

3. Installieren Sie den Host-Überwachungsdienst gruppenverwalteten Dienstkontos auf dem Knoten.

   ```powershell
   Install-ADServiceAccount -Identity <HGSgMSAAccount>
   ```
