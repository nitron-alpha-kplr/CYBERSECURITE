# CYBERSECURITE

CAPTAIN LOG DU 17 07 2023 :

Plan du cours
1
Jour 1 : Concepts introductifs
•Définition et terminologie
•Histoire
•Statistiques
•Carrières en cybersécurité
•Introduction à la cryptographie
•Types de cryptographie
•Hachage
•Encodage
•Cryptographie Symétrique
•Cryptographie Asymétrique
•Signature (en bref)
•Certificat (en bref)
•Applications de la cryptographie
•Signature numérique
•Authentification
Jour 2 : Stéganographie
• Introduction à la stéganographie
• Définition de la stéganographie
• Histoire de la stéganographie
• Utilisations de la stéganographie
• Techniques de stéganographie
• Stéganographie dans les images
• Stéganographie dans les fichiers audio
• Stéganographie dans les textes
• Stéganographie utilisant la cryptographie
• Détection de la stéganographie
• Méthodes de détection de la stéganographie
• Outils de détection de la stéganographie
• Contre-mesures de la stéganographie
• Applications de la stéganographie
Plan du cours

2
DéfinitionA
Définition de la cybersécurité
Cyber-
Préfixe
Définition :
Connecté aux réseaux de communication
électronique, notamment l'internet.*1
Origine :
Mot en Anglais
Cybernetics → Cyber- (1960s)
Traduction :
Informatique
Sécurité
Nom féminin
Définitions :
1. État d'esprit confiant et tranquille d'une personne qui se
croit, se sent à l'abri du danger.
2. Situation tranquille qui résulte de l'absence réelle de
danger.
3. Sécurité sociale (en France) mesures et organisation pour
garantir les individus contre certains risques (risques
sociaux).
4. Absence ou faiblesse relative d'accidents.
5. Dispositif qui empêche de manœuvrer intempestivement
un appareil.
Cybersécurité
Codage en Base64
Exemple : Coder le mot "Hi" en base 64
Le codage du mot "Hi" en base64 est : SGk=
Preuve :
Voici la preuve binaire de la conversion du mot "Hi" en base64 :
1. Conversion des caractères en code ASCII :
"H" : 72 (01001000 en binaire)
"i" : 105 (01101001 en binaire)
2. Concaténation des codes ASCII pour former une chaîne binaire :
01001000 01101001
3. Division de la chaîne binaire en blocs de 6 bits :
010010 000110 1001
4. Ajout de zéros à la fin pour compléter le dernier bloc :
010010 000110 100100
5. Conversion de chaque bloc de 6 bits en décimal :
18 6 41
6. Encodage de chaque valeur décimale en caractère base64, en utilisant la table de
correspondance :
18 : S
6 : G
41 : k
7. Concaténation des caractères encodés pour former la chaîne finale :
SGk=
Table de correspondance :
Voici la table de correspondance utilisée pour la conversion d'une chaîne binaire en
base64. Elle attribue un caractère spécifique à chaque valeur décimale possible pour un
bloc de 6 bits, de 0 à 63 :
Valeur décimale Caractère base64
0 A
1 B
Méthodes de cryptographie
Termes clés (Rappel) :
1
Texte en clair
( Plain text )
Hachage
Chiffrement par clé
Digest ou Empreint
Texte chiffré (ciphertext)
Atelier 2 - Chiffrement Symétrique

Atelier 2 - Chiffrement Symétrique
Lien : https://tryhackme.com/room/cryptographyintro
Objectif : Déchiffrer 3 fichiers chiffrés par des algorithmes de cryptographie (AES256, AES256-CBC et CAMELLIA256).
Outils : gpg, openssl
Durée : 40 minutes


Il existe de nombreux programmes disponibles pour le chiffrement symétrique. Nous nous concentrerons sur deux d'entre eux, qui sont également largement utilisés pour le chiffrement asymétrique :

Garde de confidentialité GNU
Projet OpenSSL


Garde de confidentialité GNU
Le GNU Privacy Guard , également connu sous le nom de GnuPG ou GPG, implémente la norme OpenPGP.



Nous pouvons chiffrer un fichier à l'aide de GnuPG (GPG) à l'aide de la commande suivante :



gpg --symmetric --cipher-algo CIPHER message.txt


où CIPHER est le nom de l'algorithme de chiffrement. Vous pouvez vérifier les chiffrements pris en charge à l'aide de la commande `gpg --version`. Le fichier crypté sera enregistré en tant que `message.txt.gpg`.



La sortie par défaut est au format binaire OpenPGP ; cependant, si vous préférez créer une sortie blindée ASCII, qui peut être ouverte dans n'importe quel éditeur de texte, vous devez ajouter l'option `--armor`. Par exemple,



gpg --armor --symmetric --cipher-algo CIPHER message.txt


Vous pouvez déchiffrer à l'aide de la commande suivante :



gpg --output original_message.txt --decrypt message.gpg


Projet OpenSSL


Le projet OpenSSL maintient le logiciel OpenSSL.



Nous pouvons chiffrer un fichier en utilisant OpenSSL en utilisant la commande suivante :



openssl aes-256-cbc -e -in message.txt -out encrypted_message


Nous pouvons déchiffrer le fichier résultant à l'aide de la commande suivante :



openssl aes-256-cbc -d -in encrypted_message -out original_message.txt


Pour rendre le chiffrement plus sûr et plus résistant aux attaques par force brute, nous pouvons ajouter `-pbkdf2`la fonction de dérivation de clé basée sur le mot de passe 2 (PBKDF2) ; de plus, nous pouvons spécifier le nombre d'itérations sur le mot de passe pour dériver la clé de chiffrement en utilisant `-iter NUMBER`. Pour itérer 10 000 fois, la commande précédente deviendrait :



openssl aes-256-cbc -pbkdf2 -iter 10000 -e -in message.txt -out encrypted_message


Par conséquent, la commande de déchiffrement devient :



openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in encrypted_message -out original_message.txt


Dans les questions suivantes, nous utiliserons `gpg` et `openssl` sur l'AttackBox pour effectuer un chiffrement symétrique.



Les fichiers nécessaires à cette tâche se trouvent sous `/root/Rooms/cryptographyintro/task02`. 



Veuillez passer au test suivant pour répondre aux questions de l'atelier.
Atelier 3 - Chiffrement Asymétrique
Lien :  https://tryhackme.com/room/cryptographyintro
Objectif : Déchiffrer un message reçu d'Alice en utilisant la clé privée.
Outils : openssl
Durée : 40 minutes
RSA
RSA tire son nom de ses inventeurs, Rivest, Shamir et Adleman. Cela fonctionne comme
suit :
1. Choisissez deux nombres premiers aléatoires, p et q . Calculez N  =  p  ×  q .
2. Choisissez deux entiers e et d tels que e  ×  d  = 1 mod φ ( N ) , où φ ( N ) =  N  −  p  
−  q  + 1 . Cette étape va nous permettre de générer la clé publique ( N , e ) et la clé
privée ( N , d ) .
3. L'expéditeur peut chiffrer une valeur x en calculant y  =  x e mod N . (module)
4. Le destinataire peut déchiffrer y en calculant x  =  y d mod N . Notez que y ré  =  X e ré
 =  X k φ ( N ) + 1
 = ( X φ ( N )
) k  ×  X  =  X . Cette étape explique pourquoi nous avons
mis une restriction sur le choix de e et d .
Ne vous inquiétez pas si les équations mathématiques ci-dessus semblent trop
compliquées ; vous n'avez pas besoin de mathématiques pour pouvoir utiliser RSA, car il
est facilement disponible via des programmes et des bibliothèques de programmation.
La sécurité RSA repose sur le fait que la factorisation est un problème difficile. Il est facile
de multiplier p par q ; cependant, il faut du temps pour trouver p et q étant donné N . De
plus, pour que cela soit sûr, p et q doivent être des nombres assez grands, par exemple,
chacun étant de 1024 bits (c'est un nombre avec plus de 300 chiffres). Il est important de
noter que RSA s'appuie sur la génération sécurisée de nombres aléatoires, comme avec
d'autres algorithmes de chiffrement asymétriques. Si un adversaire peut deviner p et q ,
l'ensemble du système serait considéré comme non sécurisé.
Considérons l'exemple pratique suivant.
1. Bob choisit deux nombres premiers : p  = 157 et q  = 199 . Il calcule N  = 31243 .
