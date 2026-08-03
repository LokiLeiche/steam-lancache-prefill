# prefill

<div data-cli-player="../casts/prefill.cast" data-rows=13></div>
<br>

## Übersicht

Füllt einen Lancache-Server autmatisch mit {{ gaming_service_name }} Spielen, sodass zukünftige Downloads von Lancache direkt beantwortet können, was Geschwindigkeiten erhöhen und die Netzwerkauslastung verringern kann.

Speichert zuvor heruntergeladene Spiele und lädt beim erneuten Ausführen nur Spiele herunter, für die neue Versionen verfügbar sind.

-----

## Beispiel

!!! Achtung
    Dieser Befehl lädt automatisch alle Apps herunter, die mit dem Befehl `select-apps` ausgewählt wurden, unabhängig von zusätzlichen Optionen.

Um den `prefill` Prozess zu starten, muss einfach nur der folgende Befehl im Terminal eingegeben werden:
```powershell
./{{prefill_name}} prefill
```

Nach Beginn des `prefill` Befehl, prüft **{{prefill_name}}**, welche Apps seit dem letzten ausführen neue Versionen erhalten haben, oder noch nie erfolgreich heruntergeladen wurden. Wenn `prefill` eine solche App erkennt, beginnt es mit dem Download. Falls keine Apps heruntergeladen werden müssen, beendet der Prozess sich selbst.


### Deine komplette {{gaming_service_name}} Bibliothek herunterladen

Je nachdem wie groß deine Bibliothek ist und wie viele Apps du herunterladen willst, könnte es einfacher sein, die komplette Bibliothek herunterzuladen, anstatt die Apps einzeln mit dem Befehl `select-apps` auszuwählen. Dadurch werden auch neu gekaufte Apps direkt mit aufgenommen und mpssen nicht manuell mit `select-apps` nach dem Kauf hinzugefügt werden.

```powershell
./{{prefill_name}} prefill --all
```

### Sicherstellen, dass der Cache vollständig gefüllt ist

Wenn beispielsweise bald ein Event ansteht und du zu 100% sicher sein willst, dass alle Apps und alle Updates heruntegeladen und im Lancache zwischengespeichert wurden, kannst du diesen Befehl verwenden. Normalerweise sollte `prefill` alle ausgewählten apps immer mit allen aktuellen Updates herunterladen, durch verschiedene Gründe könnten apps nicht mehr zwischengespeichert sein, auch wenn sie das eigentlich sollten. Mit der zusätzlichen Option `--force` wird **{{prefill_name}}** gezwungen, alle Apps erneut herunterzuladen, auch wenn sie schon zwischengespeichert sind. Dadurch dass alle Apps vollständig neu heruntergeladen werden, werden sämtliche fehlenden Dateien ergänzt.

```powershell
./{{prefill_name}} prefill --force
```

### Mehrere Optionen kombinieren

Es ist möglich mehrere Optionen in einem einzelnen Befehl zu kombinieren, anstatt jede einzeln zu verwenden. Der folgende Befehl wählt beispielsweise die meistgespielten Spiele von Steam aus, lädt nur die Linux version herunter und gibt zusätzlich mehr Details aus:

```powershell
./{{prefill_name}} prefill --top --os linux --verbose
```

-----

## Options

| Option &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | &nbsp; &nbsp; | Values                | Default     |     |
| ------------------------------------------------------------------------------------------------- | ------------- | --------------------- | ----------- | --- |
| --os                                                                                              |               | windows, linux, macos | **windows** | Specifies which operating system(s) games should be downloaded for.  Typically, almost all games support Windows, however there are increasingly more games that have Linux specific game files.  In some cases, the Linux game files may be as large as the Windows version. |
| --all                                                                                             |               |                       |             | Downloads all owned apps, useful for prefilling a completely empty cache.  |
| --recent                                                                                          |               |                       |             | Adds any games played within the last 2 weeks to the download queue.  |
| --recently-purchased                                                                              |               |                       |             | Prefill will include all games purchased in the last 2 weeks. |
| --top                                                                                             |               | 1-100                 | **50**      | Downloads the most popular games by player count, over the last 2 weeks.  |
| --force                                                                                           | -f            |                       |             | By default, **{{prefill_name}}** will keep track of the most recently prefilled apps, and will only attempt to prefill if there it determines there a newer version available for download.  This default behavior will work best for most use cases, as no time will be wasted re-downloading files that have been previously prefilled.  <br/><br/> Running with the flag `--force` will override this behavior, and instead will always run the prefill, re-downloading all files for the selected apps.  This flag may be useful for diagnostics, or benchmarking network performance.  |
| --verbose                                                                                         |               |                       |             | Produces more detailed log output.  By default, games that are already up to date will not be displayed at all.  Specifying this option will make it so that all games, even ones up to date, will be logged.  |
| --unit                                                                                            |               | bits, bytes           | **bits**    | Specifies which unit to use to display download speed.   |
| --no-ansi                                                                                         |               |                       |             | Application output will be in plain text, rather than using the visually appealing colors and progress bars.  Should only be used if terminal does not support Ansi Escape sequences, or when redirecting output to a file. |
