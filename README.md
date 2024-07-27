### 1. Erstelle ein neues Repository auf GitHub, GitLab oder Bitbucket

- Gehe zu der von dir bevorzugten Git-Hosting-Plattform.
- Erstelle ein neues Repository. Gib ihm einen passenden Namen, zum Beispiel `parent-repo`.

### 2. Initialisiere das übergeordnete Repository lokal (falls noch nicht geschehen)

Falls du es noch nicht gemacht hast:
```bash
cd path/to/your/parent-folder
git init
```

### 3. Füge die Submodule hinzu

Falls du es noch nicht gemacht hast:
```bash
git submodule add <URL_TO_FRONTEND_REPO> frontend
git submodule add <URL_TO_BACKEND_REPO> backend
```

### 4. Füge das entfernte (remote) Repository hinzu

Verbinde dein lokales Repository mit dem entfernten Repository, das du auf der Git-Hosting-Plattform erstellt hast:
```bash
git remote add origin <URL_TO_PARENT_REPO>
```
Ersetze `<URL_TO_PARENT_REPO>` durch die URL des neuen, leeren Repositories, das du erstellt hast.

### 5. Änderungen committen und pushen

Committe deine Änderungen und pushe sie in das entfernte Repository:
```bash
git add .
git commit -m "Initial commit with submodules"
git push -u origin master
```

### 6. Klonen des übergeordneten Repositories auf dem neuen PC

Auf deinem neuen PC klonst du nun das übergeordnete Repository und initialisierst die Submodule:
```bash
git clone <URL_TO_PARENT_REPO>
cd parent-folder
git submodule update --init --recursive
```

---

Wenn du mit einem übergeordneten Repository und Submodulen arbeitest, gibt es einige Best Practices und spezifische Schritte, die du beachten solltest, um die Synchronisation und Verwaltung deiner Repositories reibungslos zu gestalten. Hier sind die empfohlenen Vorgehensweisen:

### 1. Änderungen im Submodul vornehmen
Wenn du Änderungen im Frontend- oder Backend-Repository vornimmst, behandelst du sie weitgehend wie separate Repositories:

1. **Wechsle in das Submodul-Verzeichnis**:
   ```bash
   cd frontend
   ```

2. **Änderungen vornehmen und committen**:
   ```bash
   git add .
   git commit -m "Deine Änderungsbeschreibung"
   ```

3. **Änderungen pushen**:
   ```bash
   git push origin main  # oder der entsprechende Branch
   ```

### 2. Änderungen im übergeordneten Repository aktualisieren
Da Submodule als spezifische Commits des jeweiligen Repositories im übergeordneten Repository referenziert werden, musst du das übergeordnete Repository aktualisieren, nachdem du Änderungen in einem Submodul gepusht hast.

1. **Zurück ins übergeordnete Repository**:
   ```bash
   cd ..
   ```

2. **Übergeordnetes Repository aktualisieren**:
   ```bash
   git add frontend
   git commit -m "Updated frontend submodule"
   ```

3. **Änderungen pushen**:
   ```bash
   git push origin main  # oder der entsprechende Branch
   ```

### 3. Änderungen von anderen Entwicklern übernehmen
Wenn andere Entwickler Änderungen in den Submodulen vornehmen und diese ins übergeordnete Repository pushen, musst du sicherstellen, dass du diese Änderungen korrekt übernimmst.

1. **Pull im übergeordneten Repository**:
   ```bash
   git pull origin main  # oder der entsprechende Branch
   ```

2. **Submodule aktualisieren**:
   ```bash
   git submodule update --recursive --remote
   ```

### 4. Best Practices für den Umgang mit Submodulen

1. **Regelmäßig Submodule aktualisieren**: Vergewissere dich, dass deine Submodule stets aktuell sind, indem du regelmäßig `git submodule update` ausführst.
2. **Arbeiten in den Submodulen**: Behandle Submodule wie unabhängige Repositories. Committe und pushe Änderungen direkt in den Submodulen.
3. **Commit im übergeordneten Repository nach Submodul-Änderungen**: Vergiss nicht, das übergeordnete Repository zu committen, nachdem du Änderungen in einem Submodul gemacht und gepusht hast.
4. **Übergeordnetes Repository aktuell halten**: Pull und Push im übergeordneten Repository sollten stets mit einem Update der Submodule begleitet werden.

### Zusammenfassung der Befehle

**Änderungen im Frontend-Submodul**:
```bash
cd frontend
git add .
git commit -m "Deine Änderungsbeschreibung"
git push origin main
cd ..
git add frontend
git commit -m "Updated frontend submodule"
git push origin main
```

**Änderungen vom übergeordneten Repository übernehmen**:
```bash
git pull origin main
git submodule update --recursive --remote
```

Durch die Beachtung dieser Schritte und Best Practices stellst du sicher, dass deine Arbeit mit einem übergeordneten Repository und Submodulen effizient und organisiert bleibt.
