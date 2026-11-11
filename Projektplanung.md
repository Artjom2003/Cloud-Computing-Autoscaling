# Projektplanung – Projekt 8: Autoscaling mit HPA, VPA und KEDA

Modul Cloud Computing, HS Flensburg, Prof. Ralf Lübben, WS 2026/27

Team: Catharina Thomsen, Artjom Wagner

---

## 9.11.

### Projektidee

Wir betrachten einen Online-Shop mit schwankender Last – vom ruhigen Tag bis zur Lastspitze wie am Black Friday.

- Das **Shop-Frontend** bekommt bei vielen Besuchern mehr Pods, abhängig von der CPU-Last (**HPA**).
- **Bestellungen** landen in einer Warteschlange und werden von Workern abgearbeitet. Die Anzahl der Worker richtet sich
  nach der Länge der Warteschlange, bei leerer Warteschlange bis auf null (**KEDA**).
- Der **VPA** empfiehlt, wie viel CPU und Arbeitsspeicher die Pods tatsächlich brauchen.

Die Last erzeugen wir mit einem Lastgenerator (simulierte Kunden) bzw. einem Skript, das Bestellungen in die Warteschlange schreibt.
Als Anwendungen planen wir die Online Boutique (Open-Source-Demo-Shop mit eingebautem Lastgenerator) und eine Redis-Liste mit
Worker-Deployment. Passt der Shop nicht in unseren Laborcluster, weichen wir auf eine kleinere Beispielanwendung aus (z. B. php-apache).

Gemeinsames Ziel: Die Lösung lässt sich mit der README auf einem frischen Cluster installieren, und wir zeigen mit Lasttests
und Diagrammen, wie schnell die Skalierung reagiert und wann sie an Grenzen stößt.

### Arbeitspakete und Ergebnisse pro Person

**Catharina Thomsen – Paket A (HPA) und Teil von Paket C (VPA)**

| Arbeitspaket | Ergebnis im Repository |
|---|---|
| metrics-server und Shop installieren | Installationsskripte und YAML-Dateien im Ordner `hpa/` |
| HPA für das Shop-Frontend nach CPU-Auslastung | HPA-Konfiguration in `hpa/` |
| Lasttests mit unterschiedlicher Last, Messung von Hoch- und Herunterskalieren | Lasttest-Skript, Messdaten und Diagramme in `hpa/` |
| Feinabstimmung des HPA (z. B. Stabilisierungsfenster) | Vergleichsmessung in `hpa/` |
| VPA-Empfehlungen und Zusammenspiel von HPA und VPA | VPA-Konfiguration und Auswertung in `vpa/` |
| Dokumentation | `docs/hpa.md`, `docs/vpa.md` |

**Artjom Wagner – Paket B (KEDA) und Teil von Paket C (Grenzen)**

| Arbeitspaket | Ergebnis im Repository |
|---|---|
| KEDA, Redis und Worker installieren | Installationsskripte und YAML-Dateien im Ordner `keda/` |
| Skalierung nach Länge der Warteschlange, inklusive auf null | ScaledObject-Konfiguration in `keda/` |
| Messung der Reaktionszeiten, auch Kaltstart von null auf einen Pod | Skript zum Befüllen der Warteschlange, Messdaten und Diagramme in `keda/` |
| Feinabstimmung von KEDA (z. B. Abfrageintervall, Abkühlzeit) | Vergleichsmessung in `keda/` |
| Grenzen der Skalierung (Cluster voll, zu schneller Lastanstieg) und Vergleich der Verfahren | Experimente und Auswertung in `limits/` |
| Dokumentation | `docs/keda.md`, `docs/limits.md` |

**Gemeinsam:** README mit Installationsanleitung, gemeinsames Format für Messdaten und Diagramme, Abschlusspräsentation.

Jede Person arbeitet auf eigenen Branches und in ihren eigenen Ordnern; Änderungen kommen per Pull Request mit Review auf `main`.
So ist jeder Beitrag im Git einer Person zugeordnet und eigenständig prüfbar.

### Grober Zeitplan

| Zeitraum | Ziel |
|---|---|
| bis Ende November | Anwendungen und Autoscaler installiert, erste Skalierung funktioniert |

### Feedback Ralf Lübben
- An stelle des Onlineshops, kann man eine einfache Webanwendung nehmen, hier das Ganze möglichst einfach halten
| Dezember | Lasttests und Messungen, Feinabstimmung, VPA und Grenzen |
| bis zur Präsentation | Installation auf frischem Cluster testen, Dokumentation, Präsentation |
