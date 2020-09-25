<div align="center">
    Non-Natural-Language-Processing is a general non natural language utility in JS. Currently supporting:
    - Extract variables
    - Multi language
    - No training required
</div>

## Usage

1) Load the library.
```javascript
const LIBRARIES = {
    NNLP: require("./src/NNLP")
};
```
2) Instantiate.
```javascript
const NNLP = new LIBRARIES.NNLP();
```
3) Define a corpus
```javascript
const CORPUS = [
    {
        "intent": "music.play",
        "utterances": [
            "Remets la musique",
            "Remets de la musique",
            "Mets de la musique",
            "Mets-moi de la musique",
            "Joue-moi de la musique",
            "Remets-moi de la musique",
            "Rejoue moi de la musique"
        ],
        "answers": [
            "Ok",
            "C'est parti"
        ]
    },
    {
        "intent": "music.next",
        "utterances": [
            "Musique suivante",
            "Mets la musique d'après"
        ],
        "errors": {
            "noMusic": [
                "Il n'y a plus de musiques disponibles.",
                "Votre bibliothèque ne dispose plus de musiques."
            ]
        }
    },
    {
        "intent": "music.previous",
        "utterances": [
            "Musique précédente",
            "Remets la musique d'avant"
        ]
    },
    {
        "intent": "music.pause",
        "utterances": [
            "Pose",
            "Pause",
            "Stop"
        ]
    },
    {
        "intent": "music.play.specific.name.artist",
        "utterances": [
            "Mets la musique {name} de {artist|0}",
        ],
        "answers": [
            "Très bien, voici %name% de l'artiste %artist%.",
            "OK, voici %name% de l'artiste %artist%.",
            "Voici %name% de l'artiste %artist%."
        ]
    },
    {
        "intent": "music.play.specific.name",
        "utterances": [
            "Mets la musique {name}"
        ],
        "answers": [
            "Très bien, voici %name%.",
            "OK, voici %name%.",
            "Voici %name%."
        ]
    }
];
```
4) Load the corpus.
```javascript
NNLP.loadCorpus(CORPUS);
```
5) Add actions and trigger errors if needed.
```javascript
NNLP.addAction("music.play", function(_intent, _result){
    // You can do what you want here
    console.log("Ok, je lance une musique aléatoire !");
});
NNLP.addAction("music.next", function(_intent, _result){
    // If you detect an error, you can trigger them like this.
    _result.answer = _intent.error("noMusic");
});
```
6) Let the magic happen.
```javascript
console.log(NNLP.process("Je ne sais pas quoi te demander"));
console.log(NNLP.process("Mets de la musique"));
console.log(NNLP.process("Musique suivante"));
console.log(NNLP.process("Mets la musique Crossfire"));
console.log(NNLP.process("Mets la musique No Beef de Afrojack"));
```

<br>

Created by [Antoine Duval (HeyHeyChicken)](//antoine.cuffel.fr) with ❤ and ☕ (chocolate) in [Mesnil-Panneville](//en.wikipedia.org/wiki/Mesnil-Panneville).