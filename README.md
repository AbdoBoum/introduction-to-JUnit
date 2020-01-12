### Présentation de JUnit


#### 1. Présentation générale

<p align="justify">La réalisation des tests est une partie trés importante dans le développement logiciel. Elle permet de s'assurer que notre solution se comporte comme prévu. Par exemple, prenant un agent qui se déplace dans un environnement (une matrice carrée de 20 * 20) et qui initialement positionné sur la case (0, 0). Si on a crée une méthode qui permet de déplacer l'agent, nous supposons que déplacer l'agent d'un pas vers le bas donne comme résultat la nouvelle position de l'agent qui est (1, 0). Si ce n'est pas le cas, nous disons que notre application est incorrecte.</p>

<p align="justify">Nous mesurons cette adhésion aux spécifications en testant notre application. Pour réaliser ces tests on a le choix de le faire manuellement (on exécute notre code, puis on fournit les entrées pour s'assurer que le code exécuté renvoit les sorties attendues), ou bien d'une maniére automatique (les tests automatisés sont du code qui teste un autre code). Le tableau ci-dessous présente une comparaison entre les tests manuels et les tests automatisés.</p>

| Tests manuels  |Tests automatisés   |
|---|---|
|Exécution manuelle des tests sans prise en charge d'outils externes. | Prise en charge des outils externes et exécution des tests à l'aide de ces outils d'automatisation.  |
| Les tests sont exécutés manuellement, c'est une procédure très lente et fastidieuse.  | L'automatisation exécute les tests beaucoup plus rapidement qu'un dévelepeur.  |
| Les tests manuels sont moins fiables, car ils doivent tenir compte des erreurs humaines.  | Les tests automatisés sont précis et fiables.  |

<p align="justify">JUnit est le framework le plus populaire pour la réalisation des tests automatisés pour l'écosystéme Java. Le principal intérêt est de s'assurer que le code répond toujours aux besoins même après d'éventuelles modifications. JUnit a été bifurqué en JUnit 4 et JUnit 5. Alors que JUnit 5 contient un certain nombre d'innovations intéressantes, dans le but de prendre en charge de nouvelles fonctionnalités dans Java 8 et plus, ainsi que de permettre de nombreux styles de tests différents, JUnit 4 est toujours le plus populaire, et nous sommes plus susceptibles de trouver des cas de test JUnit 4 dans la pratique. Pour cette raison, nous nous concentrerons sur la création de tests automatisés avec JUnit 4.</p>

#### 2. Procédure d’installation

Pour créer des tests avec JUnit 4, nous devons ajouter la dépendance Maven suivante à notre pom.xml:
```
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
```
Si on utilise Gradle on doit ajouter la dépendance suivante:
```
testCompile group: 'junit', name: 'junit', version: '4.12'
```
<p align="justify">Avec nos dépendances ajoutées, nous pouvons maintenant commencer à tester notre application.
<p align="justify">De plus, il existe désormais une prise en charge directe pour exécuter les tests unitaires sur la plate-forme JUnit dans Eclipse ainsi que IntelliJ. Bien entendu, nous pouvons également exécuter des tests à l'aide de l'objectif du test Maven (mvn test).</p>

> Pour ajouter manuellement JUnit 4, veuillez suivre les instructions décrites dans le lien suivant: [Cliquer ici](https://www.jetbrains.com/help/idea/configuring-testing-libraries.html).

#### 3. Fonctionnalités

<p align="justify">L'utilisation des tests automatisés permet de séparer le code de la classe, du code qui permet de la tester. JUnit permet le développement incrémental d'une suite de tests. Il propose:

1. Un framework pour le développement des tests unitaires reposant sur des assertions qui testent les résultats attendus.

1. Des applications pour permettre l'exécution des tests et afficher les résultats.

1. La création d'une instance de la classe et de tout autre objet nécessaire aux tests.

1. L'affichage de la progression des tests dans une barre qui devient verte si les test passent, et elle devient rouge lorsqu'un test échoue.

1. L'appel de la méthode à tester avec les paramètres du cas de tests.

1. La comparaison du résultat attendu (expected result) avec le résultat obtenu (actual result) : en cas d'échec, une exception est levée.

1. Des annotations pour identifier les méthodes de test.

#### 4. Les assertion

<p align="justify">Le package le plus important dans JUnit est junit.framework, qui contient toutes les classes de base. La class Assert (public class Assert extends java.lang.Object
) fournit un ensemble de méthodes d'assertion utiles pour l'écriture de tests. Une assertion est une déclaration que nous supposons être vraie à un moment précis de l'exécution du code.

Si l'assertion est vraie, le test pass, sinon il échoue. Certaines des méthodes importantes de la classe Assert sont les suivantes:

| DÉCLARATION  |DESCRIPTION   |
|---|---|
|assertTrue(condition)	|vérifie si  'condition' est vraie.|
|assertFalse(condition)	| vérifie si  'condition' est fausse.|
|assertEquals(expected, actual)	|vérifie que les deux primitives / objets sont égaux.|
|assertNotEquals(expected, actual)|vérifie que les deux primitives / objets sont différents.|
|assertNull(value)	|vérifie que 'value' est null.|
|assertNotNull(value)	|vérifie que 'value' n'est null.|
|fail() |échoue un test sans message.|

Maintenant nous allons faire une démonstration pour voir l'utilité des méthodes mentionnées ci-dessus.

#### 5. Guide d’utilisation

<p align="justify">Supposons que nous avons une class Agent (voir annexe 1) que nous voulons tester. Un agent initialement à une variable score initialisé à 0 et une variable état qui détérmine si l'agent est occupé ou non.

<p align="justify">Pour créer un test avec JUnit il suffit d'écrire une class de test (AgentsTest par exemple) et chaque test sera une méthode avec une annotation **@Test**.

<p align="justify">Commençant par un test simple qui vérifie que la création d'un agent est faite correctement:

```
public class AgentsTest {
  @Test
  public void defaultAgentCreation() {

  }
}
```
<p align="justify">Nous devons initialement créer un agent en utilisant le constructeur par défaut, puis on doit vérifier si les attributs sont initialisé correctement.

```
public class AgentsTest {
  @Test
  public void defaultAgentCreation() {
    Agent agent = new Agent();
    assertTrue(agent.isFree());
    assertEquals(0, agent.getScore());
  }
}
```

<p align="justify">Le test ci-dessus est un test classic pour un POJO. Nous pouvons ajouter d'autres tests pour vérifier si un agent customisé est crée correctement et pour vérifier que la méthode pickGold() se comporte come prévu.

```
public class AgentsTest {
  @Test
  public void defaultAgentCreation() {
    Agent agent = new Agent();
    assertTrue(agent.isFree());
    assertEquals(0, agent.getScore());
  }

  @Test
  public void customAgentCreation() {
    Agent agent = new Agent("1234", true, 5);
    assertEquals("1234", agent.getId());
    assertTrue(agent.isFree());
    assertEquals(5, agent.getScore());
  }

  @Test
  public void testGoldPicking() {
    Agent agent = new Agent();
    agent.pickGold();
    assertFalse(agent.isFree());
    assertEquals(1, agent.getScore());
  }
}
```

<p align="justify">Bien que la création de nos tests consomme la majeure partie de l'effort, les tests sans mécanisme d'exécution ne servent à rien. En règle générale, il existe 2 façons courantes d'exécuter des tests JUnit: (1) sur la ligne de commande à l'aide de Maven/Gradle, (2) à l'aide de l'IDE.

**Maven**
```
mvn test
```

**Gradle**
```
gradle test
```

**IDE**

<p align="justify">Il suffit d'éxecuter la class de test sous IntelliJ IDEA, et sous Eclipse click droit sur la classe de test, puis **RUN AS**, et enfin **JUnit Test**.

#### 6. Générer un rapport HTML

<p align="justify">Nous pouvons utiliser le plugin maven-surefire-report-plugin pour générer des rapports HTML pour nos tests unitaires. Ce rapport peut être exporté et partagé avec l'équipe. Il de comprendre le déroulement des tests, et il est utile en cas d'utilisation d'un outil d'intégration continue (CI).
    
Pour ce faire, il suffit de tapper la commande: 
> mvn surefire-report:report

Un rapport HTML doit être généré dans ${basedir}/target/site/surefire-report.html.

![Test report](https://github.com/AbdoBoum/introduction-to-JUnit/blob/master/tests-report.png)



#### Conclusion
<p align="justify">Les tests unitaires sont une facette essentielle du développement logiciel, et les tests automatisés sont une partie cruciale des tests. Pour l'écosystéme Java, JUnit est le cadre de référence pour la création de tests unitaires automatisés, en raison de sa simplicité et de sa prise en charge par la plupart des IDE - tels que Eclipse et IDEA - et des systèmes de construction - tels que Maven et Gradle.

#### Annexe

1. La class Agent:

```
public class Agent implements {

    private String id;
    private boolean free;
    private int score;

    public Agent() {
        this(UUID.randomUUID().toString(), true, 0);
    }

    public Agent(String id, boolean free, int score) {
      this.id = id;
      this.free = free;
      this.score = score;
    }

    // ... getters & setters ...

    public void pickGold() {
      this.free = false;
      score += 1;
    }

```
