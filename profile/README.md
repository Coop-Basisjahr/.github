# Coop Basisjahr Verwaltung

Diese Organisation dient dazu, Repositories Lehrjahrübergreiffend zu verwalten. Alle Repositories dienen als Vorlage. Es gibt folgende Arten von Repositories:

- Handouts: Eine Sammlung von allen Handouts und Übungen der verschiedenen Themen, welche im Basisjahr behandelt werden.
- Demo: Beispielcode zu einem Thema.
- Übung: Beinhalten den Startercode für ein GitHub Classroom Assignment.
- Solution: Beinhalten die Musterlösung zu einer Übung.

## Handouts

Im Handout-Repository dieser Organisation sind alle Handouts, zu allen bisher behandelten Themen. Sie dienen als Backlog für das Zusammenstellen der Inhalte für ein neues Lehrjahr.

## Demos

Demo Repositories werden üblicherweise bei einem Input eines Themas präsentiert. Das Repo kann in die Organisation des Lehrjahrs kopiert werden, damit Lernende den Code anschauen können.
Teile dieses Codes sind typischerweise in den Handouts zu finden.

## GitHub Classroom

Um ein Classroom Assignment zu erstellen, braucht es ein `uebung__` und `solution__` Repository. Die Repositories müssen bis auf den Prefix gleich heissen. Z.B.

- `uebung__my-assignment`
- `solution__my-assignment`

Das Übungsrepository muss ausserdem ein Template und public sein und das Lösungsrepository sollte auf private gestellt sein.

Nun kann auf GitHub Classroom ein Assignment erstellt werden mit dem Übungsrepository als Starter Code. GitHub Classroom erstellt in der Organisation des Lehrjahrs eine Kopie des Starter Repos und für alle Lernenden einen persönlichen Fork dieser Kopie.

### Übung und Lösungen erstellen

Füge folgende Bash Function in die Datei `~/.zshrc` ein. Nenne sie bei Bedarf um.

```bash
pull() {
    git clone https://github.com/Coop-Basisjahr/uebung__$1.git
    mv uebung__$1 $1
    cd $1
    git remote add solution https://github.com/Coop-Basisjahr/solution__$1.git
    git branch solution
    git checkout solution
    git fetch solution
    git reset --hard solution/main
    git branch --set-upstream-to solution/main
    git config push.default "upstream"
}
```

Wenn es nun von einer Übung ein `uebung__` und `solution__` Repository gibt, können diese mit z.B. `pull my-assignment` geclont werden. Das Script erstellt ein neues Repository mit zwei Branches.

- `main` ist mit dem Übungsrepository verknüpft.
- `solution` ist mit dem Übungsrepository verknüpft.

Bearbeite die Übung und Lösung lokal und pushe die Branches wie gewohnt.
