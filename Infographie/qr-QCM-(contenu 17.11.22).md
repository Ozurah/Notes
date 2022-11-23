En quoi maîtriser la notion de matrice est-il important pour WebGL ?	
	Les transformations (c'est-à-dire : déplacement/rotation/scale) se font par multiplication de matrices

Combien faut-il de matrice pour simuler la camera sous WebGL ?	
	"• Position, orientation  model view matrix
	• Angle de vue – ou pas + espace plan min et plan max  projection matrix"

À quoi sert la matrice communément appelée « mvMatrix » ?	
	représenter le modèle dans l'espace

À quoi sert la matrice communément appelée « pMatrix » ?	
	Représenter la caméra

Citer une similarité entre GLSL et CUDA.	
	Les deux utilisent les GPU pour les calculs

Citer une différence entre GLSL et CUDA.	
	GLSL produit des images // CUDA seulement des calculs

Quel est l’avantage de l’approximation de sphère par insertion d’équations dans le Fragment Shader.	
	Très peu de triangles (2)

Dans  quelle  fonction  fondamentale  retrouve-t-on  le  mot  clé  écrit  ainsi  <objet  contexte graphique>.TRIANGLES ?	
	La façon de lier les différent vertex entre eux (drawScene) dans la fonction webgl drawElements

Citer une instruction définissant la géométrie d’un objet composé d’un triangle.	
	fonction webgl bindBuffer

A quoi sert l'instruction gl_PointSize	
	specify the diameter of rasterized points

Décrire la nature des objets générés par TRIANGLE_STRIP	
	Objet continu car les triangles partagent toujours 2 sommet???

Qu'est-ce qu'un TRIANGLE_FAN	
	Le Triangle fan est une primitive de dessin 3D qui décrit des triangles connectés partageant un sommet commun

Quel type de rendu nécessite l’utilisation de la technique render-to-texture ?	
	camera to texture (in game TV) ?? reflection ??

Dans quelle partie du code doit-on placer le code calculant le modèle d'illumination de Phong ?	
	fragment shader ?? 

Quelle est la nature du repère des objets au sein du Fragment Shader ?	
	Repère discret généralement lié au pixel à l'écran (viewport)

Qu'est-ce que le repère canevas ?	
	c'est celui qui est affiché sur la page html, il est calculé en pixels

Quelle instruction doit impérativement conclure le Fragment Shader ?	
	mettre la couleur sur le vec 4 out (  GLFragColor = vColor;)

À quoi sert le "Vertex Shader" ?	
	Transformée par rapport au repère caméra -> position

À quoi sert le "Fragment Shader" ?	
	à colorer les pixels (fragment)

Quelle instruction doit impérativement conclure le Vertex Shader ?	
	gl_Position = <valeur de type vec4>

Choisir un exemple de typage valide en GLSL.	
	uniform vec4 uColor;

GLSL requiert quel type de typage ?	
	Le double typage

Définir le type varying.	
	Valeur qui va être interpolée entre le passage vertex shader --> fragment shader (par exemple : un vecteur représentant une couleur pour créer un dégradé entre les vertex)

Définir le type mat4.	
	Matrice 4x4

Définir le type uniform .	
	Variable ayant une valeur définie, indépendemment des vertex, on utilise un uniform si l'on souhaite passé une variable de notre code JS à la carte graphique

Définir le type attribute.	
	Valeur spécifique au vertex actuel (par exemple : récupération de la position/couleur/normal du vertex actuel)

Comment passer un float de vertex à un fragment ?	
	"Si la valeur doit varier entre les vertex par interpolation :
	        varying
	Si la valeur est la même/rester uniforme pour tous les vertex (et donc pour tous les fragments) :
	        uniform"

Comment réaliser le rendu d’une sphère parfaite (i.e. sans polygone visible) ?	
	Modèle 3D : deux triangles formant un carré, visuel de la sphère réalisé dans le shader

Comment récupérer la position (x,y) d’un pixel traiter dans le Fragment Shader ?	
	avec l'attibut webgl gl_FragCoord (vec2), représente les coordonées x,y du millieu du pixel sur l'écran.

Donner une courte définition de la technique render-to-texture.	
	Methode permmettant de générer des textures avec des effet calculé par GPGPU

Donner la déclaration d’un float formant un pont du Vertex au Fragment Shaders.	
	varying float vMyFloat;

Donner la déclaration d’un tableau à deux dimensions de vecteur de float distribué à tous les GPUs.	
	uniform vec2 uMyTab

Donner la déclaration d’un tableau à deux dimensions de vecteur de float distribué unitairement à chaque les GPUs.	
	in vec2 aMyTab

Quelle est la déclaration d’un tableau de vecteur de réel à deux dimensions distribué unitairement à chaque les GPUs ?	
	in dvec2 aMyTab

Quelle est la déclaration d’un vecteur entier à quatre dimensions distribué à tous les GPUs ?	
	uniform ivec4 uMyTab

Quelle est la déclaration dans les deux Shaders d’un float formant un pont indirect entre ceux-ci en WebGL 1.0.	
	"vertex: out float vMyFloat
	fragment: in float vMyFloat"

Expliquer la terminologie attribute ivec3 aMyVar	
	tableau de vecteur de trois entier distibué unitairement au GPU

Quelle est la taille du tableau d’indice pour un tétraèdre si on utilise une bande de triangle ?	
	N+2

Quelle est la taille du tableau d’indice pour un tétraèdre si on utilise une série de triangles ?	
	3N

Quel est le rôle fondamental de la fonction initShaderParameters(< nom shader prog> ) ?	
	Créer un pont pour le partage d'informations entre le CPU (html + js) et le GPU (shaders)

Expliquer le code suivant uniform mat4 uMyVar	
	création d'un uniform de type matrice 4x4 

Expliquer le code suivant varying vec4 vMyVar	
	création d'un varying de type vecteur à 4 composantes

Quel repère défini côté JS permet la projection des zones de textures sur les triangles ?	
	canvas?

Quelles sont les différences entre les termes de typage suivants : uniform et attribute ?	
	"- uniform are per-primitive parameters (constant during an entire draw call) ;
	- attribute are per-vertex parameters (typically : positions, normals, colors, UVs, ...) ;
	- varying are per-fragment (or per-pixel) parameters : they vary from pixels to pixels.
	https://stackoverflow.com/questions/17537879/in-webgl-what-are-the-differences-between-an-attribut"

En quoi WebGL implique, dans la majorité des cas, une interaction homme machine ?	
	WebGL produit des images celle-ci ne sont utile que pour une utilisation par l'homme

Pourquoi utiliser le terme fragment dans fragment shader ?	
	car on fragmente l'espace continu des vecteurs en pixel discret (discrétisation)

Pour quel type de rendu utilise-t-on les mots clés LINES ou LINE_STRIP ?	
	Rendu de squelette, debug

Comment est-il possible de dessiner un cercle avec seulement un triangle ?	
	Modèle 3D : deux triangles formant un carré, visuel du cercle réalisé dans le shader

En quoi connaitre CSS n’est pas une obligation pour le développement WebGL ?	
	Seul un <canvas> (HTML) et un script (JS) est nécessaire pour avoir qque chose à l'écran

En quoi connaitre html est fondamental pour le développement WebGL ?	
	Le rendu se fait dans la balise <canvas>

En quoi connaitre JS est une obligation pour le développement WebGL ?	
	C'est depuis nos scripts JS que l'on va communiquer avec la carte graphique via l'API WebGL

Pourquoi le fonction drawScene() est-elle fondamentale ?	
	parce que c'est elle qui dessine la scène, au coeur du rendu

En quoi chaque fragment d’un triangle peut-il être considéré comme un mélange unique de ses sommets ?	
	parce qu'on colorie les fragment en se basant sur les distances et valeurs des sommets

A l’entrée du Vertex Shader le format de variables peut être de quels types ?	
	atrribut et uniform (pas sûr de ce que "format" veut dire), vec3 ou vec4

A l’entrée du Fragment Shader le format de variables peut être de quels types ?	
	vec4

L’axe Z du point de vue de l’utilisateur de l’application Web est toujours …	
	Au loin (-Z), allant dans la direction de l'utilisateur (+Z), avec l'origine XYZ au millieu du viewport

Au coeur de WebGL se trouve la bibliothèque graphique intitulée…	
	OpenGL|ES

Quand on développe la transformation géométrique d’un point via une série de matrices, il ne faut pas oublier que l’ordre doit…	
	inversé l'ordre des matrices pos = P x V x M x point

Si la compilation du programme contenant les Shaders ne fonctionne pas …	
	c'est la💩

Que peut-on obtenir en retour de la compilation à la volée côté carte graphique lors que celle-ci n’a pas fonctionnée ?	
	[VIDE]

A quoi sert la fonction renderLoop() ?	
	Elle sert a afficher la scène

Comment est-il possible que la boucle de rendu ne s’arrête jamais tout en permettant à l’utilisateur d’interagir ?	
	la méthode possède un callback pour être invoqué avant le repaint, comme ça les modifications sont prise en compte pour la frame suivante (cf : Window.requestAnimationFrame())

Au sein de l’objet du contexte graphique (fréquemment déclaré sous le nom glContext), à quoi sert la méthode bindBuffer() ?	
	à dire qu'on va utiliser les données qui sont dans ce buffer là

Quel paramètre est attendu par la méthode activeTexture() ?	
	⁉️

A quoi sert la méthode bindTexture() ?	
	Elle sert a lier une texture a un objet

Est-ce que la méthode drawElement () peut-elle être appelée plusieurs fois de suite en variant le type et/ou les objets à rendre ?	
	⁉️

Lors du développement, comment peut-on tester localement la lecture et l’écriture de fichier tels que des textures sous forme d’images ou des fichiers de description géométrique (.json) ?	
	deployer un petit server pour faire du hot reload

A quoi sert la fonction <context graphique>.clearColor(<RGBa>) ?	
	pourquoi clear des buffer de couleur ? pour éviter d'éventuel problème de mauvaises couleurs

Comment signaler au pipeline de rendu que l’on souhaite que l’ordre de profondeur soient certifié ?	
	avec glContext.enable(glContext.DEPTH_TEST)

A quoi sert la méthode glContext.viewport() ?	
	"Si on ne veut pas faire le rendu sur tous le canvas, exemple on utiliserais plusieurs viewport dans le même canvas
	- (v1, v2, v3 == viewport 1, 2, 3) (en bleu foncé le canvas)"

Comment pourrait-on utiliser le même canevas pour réaliser quatre points de vue différents de la même scène ?	
	"en jouant sur la taille du viewport qu'on met dans le canevas (pour qu'il prenne pas toute la place)
	avec glContext.viewport(0, 0, c_width, c_heigh);"

Où retrouve-t-on les termes gl_FragColor et gl_Position ?	
	"gl_FragColor --> Dans le fragment shader
	gl_Position --> Dans le vertex shader"

Dimension d'un vecteur/matrice	
	1D/2D

Formes célèbres ?	
    Stanford bunny	
    Utah Teapot	


Dimension d'un vecteur/matrice

Formes célèbres ?
    Stanford bunny
    Utah Teapot

2 pyramides parfaite ? Cone et tetraedre