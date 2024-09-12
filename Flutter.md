### Cours Complet pour Débutant sur le Framework Flutter

---

Flutter est un framework open-source développé par Google, conçu pour créer des applications mobiles, web et de bureau à partir d'une seule base de code. Il utilise le langage Dart et offre une interface utilisateur moderne et réactive, construite avec des **widgets**.

---

## 1. **Introduction à Flutter et Dart**

Flutter repose sur Dart, un langage de programmation simple à prendre en main. Avant de commencer avec Flutter, il est important de comprendre certains concepts clés de Dart :

- **Syntaxe de base** : Dart utilise une syntaxe similaire à d'autres langages comme JavaScript et Java.
- **Types de variables** : Dart est typé, ce qui signifie que vous devez déclarer le type de chaque variable.
  ```dart
  int age = 25;
  String name = "Flutter";
  ```

- **Fonctions** : En Dart, les fonctions peuvent avoir des paramètres positionnels et nommés.
  ```dart
  void greet(String name) {
    print("Hello $name");
  }
  ```

Flutter est un framework basé sur les **widgets**. Tout ce que vous voyez dans une application Flutter, des boutons aux mises en page, est un widget.

### **Premier projet Flutter**
Pour démarrer avec Flutter, vous pouvez utiliser **Flutter SDK** et un IDE comme **Visual Studio Code** ou **Android Studio**.

1. Installez Flutter : Téléchargez et installez Flutter depuis le site officiel.
2. Créez un nouveau projet Flutter avec :
   ```bash
   flutter create my_first_app
   ```
3. Exécutez votre projet en utilisant :
   ```bash
   flutter run
   ```

---

## 2. **Widgets et Layouts de Base**

### **Widgets de base**
Dans Flutter, tout est un widget. Voici quelques widgets de base :

- **Text** : Pour afficher du texte.
  ```dart
  Text('Hello Flutter');
  ```

- **Container** : Un widget de base pour créer des boîtes avec des styles.
  ```dart
  Container(
    color: Colors.blue,
    width: 100,
    height: 100,
  );
  ```

- **Row et Column** : Utilisés pour organiser des widgets horizontalement ou verticalement.
  ```dart
  Column(
    children: <Widget>[
      Text('First'),
      Text('Second'),
    ],
  );
  ```

### **Layouts et Alignement**
Flutter propose des outils puissants pour créer des mises en page flexibles :

- **Padding** : Gère l'espacement intérieur autour d'un widget.
  ```dart
  Padding(
    padding: EdgeInsets.all(10.0),
    child: Text('Text with padding'),
  );
  ```

- **Expanded** et **Flexible** : Redimensionnent les widgets pour occuper l'espace disponible.
  ```dart
  Row(
    children: <Widget>[
      Expanded(child: Text('Expands to fill')),
      Flexible(child: Text('Flexible widget')),
    ],
  );
  ```

---

## 3. **Interaction avec l'utilisateur**

### **Buttons et Gestes**
Flutter propose plusieurs types de boutons pour interagir avec les utilisateurs :

- **ElevatedButton** : Un bouton classique avec une élévation.
  ```dart
  ElevatedButton(
    onPressed: () {
      print("Button pressed");
    },
    child: Text('Press Me'),
  );
  ```

- **Gestures** : Utilisez `GestureDetector` pour capturer les interactions utilisateur comme le tap, le swipe, etc.
  ```dart
  GestureDetector(
    onTap: () {
      print("Container tapped");
    },
    child: Container(color: Colors.blue),
  );
  ```

---

## 4. **Saisie et Formulaires**

### **TextField**
Le widget `TextField` permet de capturer les saisies utilisateur. Vous pouvez ajouter une décoration pour rendre le champ plus intuitif.
```dart
TextField(
  decoration: InputDecoration(labelText: 'Enter your name'),
)
```

### **Formulaire avec validation**
Utilisez le widget `Form` pour gérer et valider plusieurs champs.
```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: <Widget>[
      TextFormField(
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Please enter some text';
          }
          return null;
        },
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            // Process data
          }
        },
        child: Text('Submit'),
      ),
    ],
  ),
)
```

---

## 5. **Images et Icones**

### **Images**
Pour afficher des images dans votre application Flutter :
- **Image locale** :
  ```yaml
  assets:
    - assets/my_image.png
  ```
  ```dart
  Image.asset('assets/my_image.png');
  ```

- **Image distante** :
  ```dart
  Image.network('https://example.com/image.png');
  ```

### **Icones**
Utilisez `Icon` pour ajouter des icônes à votre application.
```dart
Icon(Icons.star, color: Colors.yellow);
```

---

## 6. **Navigation entre Écrans**

Flutter permet de naviguer facilement entre plusieurs écrans avec le **Navigator**.

### **Navigation simple**
Pour passer à un autre écran :
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
```

Pour revenir à l'écran précédent :
```dart
Navigator.pop(context);
```

---

## 7. **State Management (Gestion d'État)**

Dans Flutter, la gestion de l'état est essentielle pour maintenir les données des widgets.

### **setState**
La méthode `setState()` est utilisée pour mettre à jour l'interface utilisateur lorsqu'il y a des changements dans l'état.
```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Text('Counter: $_counter')),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

---

## 8. **Animations Simples**

Flutter propose des outils pour créer des animations fluides.

### **AnimatedContainer**
Ce widget permet de créer des animations lorsqu'une propriété du conteneur change.
```dart
AnimatedContainer(
  duration: Duration(seconds: 1),
  width: _isExpanded ? 200 : 100,
  color: _isExpanded ? Colors.blue : Colors.red,
  child: GestureDetector(
    onTap: () {
      setState(() {
        _isExpanded = !_isExpanded;
      });
    },
    child: Text('Tap to animate!'),
  ),
)
```

### **Hero Animation**
Créez des transitions visuellement fluides entre deux écrans avec `Hero`.
```dart
Hero(
  tag: 'heroImage',
  child: Image.asset('assets/hero_image.png'),
)
```

---

## 9. **Consommation d'API**

Flutter permet de consommer des API REST facilement grâce à la bibliothèque **http**.

### **Appel HTTP simple**
Ajoutez `http` à votre fichier `pubspec.yaml` :
```yaml
dependencies:
  http: ^0.13.3
```

Faites une requête GET :
```dart
import 'package:http/http.dart' as http;

void fetchPosts() async {
  final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));
  print(response.body);
}
```

---

## 10. **Optimisation des Performances**

### **Utilisez `ListView.builder`**
Plutôt que d'utiliser des listes statiques, `ListView.builder` optimise le rendu des listes longues.
```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(items[index]),
    );
  },
)
```

---

## 11. **Débogage et Test**

Flutter propose des outils comme **Flutter DevTools** pour analyser et déboguer les performances, et le support de **tests unitaires** et **tests d'interface utilisateur**.

### **Test unitaire**
```dart
void main() {
  test('String should be in uppercase', () {
    String text = 'flutter';
    expect(text.toUpperCase(), 'FLUTTER');
  });
}
```

---

## Conclusion

Flutter est un framework très complet pour le développement d'applications multiplateformes. Avec une gestion efficace des états, une navigation fluide, des animations complexes et un accès simplifié aux APIs, il permet de créer des applications modernes et performantes. Pour aller plus loin, l'exploration des tests, de la performance et de l'optimisation de l'interface sera cruciale pour affiner vos compétences en tant que développeur Flutter.
