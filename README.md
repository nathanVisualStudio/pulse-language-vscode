# Pulse Language Support for VSCode

**Syntax highlighting** pour Pulse, un langage de scripting de gameplay et IA pour jeux vidéo.

## 📖 Qu'est-ce que Pulse ?

Pulse est un langage de scripting orienté **gameplay** et **intelligence artificielle** pour le développement de jeux vidéo. Il permet de définir facilement le comportement des entités (ennemis, PNJ, objets) via un système d'états et d'événements.

**Caractéristiques** :
- 🎮 Conçu pour les jeux vidéo
- 🤖 Orienté IA et comportements d'entités
- 📝 Syntaxe simple et lisible
- ⚡ Interprété par un moteur Java

## 🚀 Installation de l'extension VSCode

1. Ouvrez Visual Studio Code
2. Allez dans **Extensions** (`Ctrl+Shift+X`)
3. Recherchez **"Pulse Language"**
4. Cliquez sur **Install**

## 💻 Utiliser Pulse dans votre projet

### ⚠️ Important : Cette extension fournit UNIQUEMENT la coloration syntaxique

Pour **exécuter** du code Pulse, vous avez besoin du **moteur Pulse** (écrit en Java).

### Installation complète :

#### 1. Prérequis
- **Java 21 ou supérieur** : [Télécharger Java](https://adoptium.net/)
- **Le moteur Pulse** : [Télécharger depuis GitHub](https://github.com/nathanVisualStudio/pulse-engine)

#### 2. Télécharger le moteur Pulse
```bash
git clone https://github.com/nathanVisualStudio/pulse-engine.git
cd pulse-engine
./gradlew build
```

#### 3. Exécuter un script Pulse
```bash
java -jar pulse-engine.jar votre-script.ps
```

## 📝 Syntaxe Pulse

### Exemple : Ennemi simple
```pulse
// Définir un ennemi avec plusieurs états
entity Enemy

state idle
  on SPAWN
    print("Enemy spawned!")
  
  on TICK
    print("Idle... looking for player")

state attacking
  on TICK
    print("Attacking player!")
    attack(10)
  
  on DIE
    print("Enemy defeated!")
```

### Exemple : Garde qui patrouille
```pulse
entity Guard

state patrol
  on SPAWN
    print("Starting patrol")
  
  on TICK
    move(5)
    print("Patrolling...")

state alert
  on INTERACT
    print("Who goes there?!")
  
  on TICK
    attack(15)
```

## 🎯 Concepts clés

### 📦 Entités (Entities)
Représentent les objets du jeu : ennemis, PNJ, items...
```pulse
entity Zombie
entity Player
entity HealthPotion
```

### 🔄 États (States)
Définissent les différents comportements d'une entité.
```pulse
state idle      // Au repos
state moving    // En déplacement
state attacking // En attaque
state dead      // Mort
```

### ⚡ Événements (Events)
Déclenchent des actions dans les états.

| Événement | Description |
|-----------|-------------|
| `SPAWN` | L'entité apparaît dans le jeu |
| `TICK` | Appelé à chaque frame (60 fois/seconde) |
| `DIE` | L'entité meurt |
| `INTERACT` | Le joueur interagit avec l'entité |

### 🛠️ Actions
Fonctions disponibles dans Pulse :
```pulse
print("message")    // Afficher un message
move(speed)         // Déplacer l'entité
attack(damage)      // Attaquer
heal(amount)        // Soigner
```

## 📂 Structure d'un projet
```
mon-jeu/
├── scripts/
│   ├── enemies/
│   │   ├── zombie.ps
│   │   └── boss.ps
│   ├── npcs/
│   │   └── merchant.ps
│   └── items/
│       └── potion.ps
├── pulse-engine.jar
└── main.java
```

## 🔧 Intégration dans votre jeu Java

### Charger et exécuter un script Pulse
```java
import pulse.engine.PulseEngine;
import pulse.loader.PulseLoader;

public class Game {
    public static void main(String[] args) {
        // Charger le script
        EntityDef enemy = PulseLoader.load("scripts/enemy.ps");
        
        // Créer une instance
        EntityInstance zombieInstance = new EntityInstance(enemy);
        
        // Moteur Pulse
        PulseEngine engine = new PulseEngine();
        GameContext context = new GameContext();
        
        // Boucle de jeu
        while (gameRunning) {
            engine.tick(zombieInstance, context);
            Thread.sleep(16); // ~60 FPS
        }
    }
}
```

## 🎓 Exemples complets

### Boss avec plusieurs phases
```pulse
entity Boss

state phase1
  on SPAWN
    print("Boss appears!")
  
  on TICK
    attack(20)
    move(3)

state phase2
  on TICK
    print("Boss is enraged!")
    attack(40)
    move(6)

state dead
  on DIE
    print("Boss defeated! You win!")
```

### PNJ marchand
```pulse
entity Merchant

state waiting
  on SPAWN
    print("Welcome to my shop!")
  
  on INTERACT
    print("What would you like to buy?")

state trading
  on TICK
    print("Showing items...")
```

## ❓ FAQ

### Cette extension exécute-t-elle mon code ?
**Non.** Cette extension fournit uniquement la **coloration syntaxique** et l'**auto-complétion** dans VSCode. Pour exécuter votre code, vous devez utiliser le moteur Pulse.

### Où télécharger le moteur Pulse ?
👉 [GitHub - Pulse Engine](https://github.com/nathanVisualStudio/pulse-engine)

### Pulse fonctionne avec quels moteurs de jeu ?
Pulse est un interpréteur Java autonome. Vous pouvez l'intégrer dans :
- ✅ Projets Java purs
- ✅ LibGDX
- ✅ jMonkeyEngine
- ✅ LWJGL
- ✅ N'importe quel projet JVM (Kotlin, Scala, etc.)

### Je débute en programmation de jeux, Pulse est-il pour moi ?
Oui ! Pulse a été conçu pour être **simple et intuitif**. Si vous savez écrire :
```pulse
entity Monster
state angry
  on TICK
    attack(10)
```
Vous savez utiliser Pulse ! 🎮

## 🐛 Problèmes connus

Aucun pour l'instant. Signalez les bugs sur [GitHub Issues](https://github.com/nathanVisualStudio/pulse-language-vscode/issues).

## 📦 Ce que cette extension inclut

- ✅ Coloration syntaxique complète
- ✅ Auto-complétion pour les mots-clés
- ✅ Snippets (raccourcis de code)
- ✅ Indentation automatique
- ✅ Support des commentaires (`//`)
- ✅ Validation de syntaxe basique

## 🚀 Roadmap

- [ ] Language Server pour validation en temps réel
- [ ] Go to Definition (aller à la définition d'un state)
- [ ] Hover tooltips (documentation au survol)
- [ ] Debugger intégré
- [ ] Refactoring automatique

## 🤝 Contribuer

Les contributions sont les bienvenues !

1. Forkez le repo
2. Créez une branche (`git checkout -b feature/amelioration`)
3. Committez vos changements
4. Pushez et créez une Pull Request

## 📄 License

MIT License - voir [LICENSE](LICENSE)

## 🔗 Liens utiles

- **Extension VSCode** : https://github.com/nathanVisualStudio/pulse-language-vscode
- **Moteur Pulse (Java)** : https://github.com/nathanVisualStudio/pulse-engine *(à créer)*
- **Documentation** : *(à venir)*
- **Discord** : *(à venir)*

## 💬 Support

Des questions ? Ouvrez une [issue sur GitHub](https://github.com/nathanVisualStudio/pulse-language-vscode/issues) !

---

**Créé avec ❤️ pour la communauté gamedev**
```

## 📌 Points importants à noter pour vos utilisateurs :

### Ce que l'extension VSCode fait :
✅ Coloration syntaxique
✅ Auto-complétion
✅ Snippets
✅ Confort d'édition

### Ce que l'extension VSCode ne fait PAS :
❌ N'exécute pas le code
❌ N'inclut pas le moteur Pulse
❌ Ne compile pas les scripts

## 🚀 Prochaines étapes pour vous :

1. **Créer un repo GitHub séparé pour le moteur** :
   - `pulse-engine` : Votre code Java qui interprète les `.ps`
   - Fournissez un JAR exécutable
   - Documentation d'intégration

2. **Fournir un exemple de projet** :
```
   pulse-example-game/
   ├── scripts/
   │   └── enemy.ps
   ├── pulse-engine.jar
   └── README.md (comment lancer)
