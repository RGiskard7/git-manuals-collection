# Oh Shit, Git!?!

>ATENCIÓN: Esto no es contenido propio, es un proyecto denominado: Oh Shit, Git!?!
>- Página oficial: [Oh Shit, Git!?!](https://ohshitgit.com)
>- Repositorio GitHub: [GitHub](https://github.com/ksylor/ohshitgit)

Git es difícil: estropearlo es fácil y darse cuenta de cómo corregir tus errores es jodidamente imposible. La documentación de Git sufre del problema del huevo y la gallina, donde no puedes buscar cómo salir del lio, *a menos de que ya sepas el nombre de lo que tienes que saber* para poder arreglarlo.

Acá hay algunas horribles situaciones con las que me encontré y cómo, eventualmente, pude resolverlas *en español simple*.

## Oh shit, hice algo terriblemente mal, por favor dime que git tiene una maquina del tiempo mágica!?!
```git
git reflog
# verás una lista de todo lo que
# haz hecho en git, en todas las ramas!
# cada uno tiene un index HEAD@{index}
# busca el comando anterior al que rompio todo
git reset HEAD@{index}
# maquina del tiempo mágica
```

Puedes usar esto para recuperar cosas que borraste accidentalmente, o simplemente para borrar cosas que intentaste hacer que rompieron el repo, o para recuperate de un mal merge, o simplemente para volver a un momento donde las cosas funcionaba. Yo uso `reflog` MUCHISIMO. Mega agradecimiento para las muchiiiiismas personas que sugirieron que lo agregue.

## Oh shit, hice commit e inmediatamente me di cuenta que tenia que hacer un pequeño cambio!
```git
# realizar cambios
git add . # o agregue archivos individuales
git commit --amend --no-edit
# ahora tu último commit contiene los cambios!
# ADVERTENCIA: nunca arregles commits públicos
```

Esto suele pasarme cuando hago commit y luego corro tests/linters... y mátame, me olvide de poner un espacio antes de un signo igual. También podrías realizar el cambio como un nuevo commit y luego hacer `rebase -i` para realizar un squash the ambos cambios juntos, pero esta manera es un millon de veces más rápido.

*Advertencia: Nunca deberías arreglar commits que han sido subidos a ramas públicas/compartidas. Solo arregla commits que existan en tu copia local o la vas a pasar mal.*

## Oh shit, necesito cambiar el mensaje en mi último commit!
```git
git commit --amend
# sigue las indicaciones para cambiar el mensaje
```

Estúpidos formatos de mensajes de commits.

## Oh shit, accidentalmente hice commit de algo a master que debía haber sido en una nueva rama!
```git
# crea una nueva rama desde master
git branch nombre-de-rama
# borra el último commit de la rama master
git reset HEAD~ --hard
git checkout nombre-de-rama
# tu commit ahora vive en al nueva rama :)
```

Nota: esto no funciona si ya haz realizado el push a una rama pública/compartida, y si haz intentado otra cosa antes, podrías necesitar hacer `git reset HEAD@{number-of-commits-back}` en vez de `HEAD~`. Tristeza infinita. También, mucuuuuuchas personas sugirieron una increible manera de hacer esto más corto que no la sabía. Gracias a todos.

## Oh shit, accidentalmente hice commit a la rama equivocada!
```git
# deshaz el útlimo commit, pero deja los cambio disponibles
git reset HEAD~ --soft
git stash
# muevete a la rama correcta
git checkout nombre-de-la-rama-correcta
git stash pop
git add . # or add individual files
git commit -m "your message here";
# ahora tus cambios estan en la rama correcta
```

Mucha gente sugirió usar `cherry-pick` para esta situacion, asi que, usa la que más sentido te haga!

```git
git checkout nombre-de-la-rama-correcta
# coge el último commit de master
git cherry-pick master
# borralo de master
git checkout master
git reset HEAD~ --hard
```

## Oh shit, trate de realizar un diff pero no pasó nada?!

Si sabes que hiciste cambios a tus archivos, pero `diff` está vacío, probablemente hiciste `add` de tus archivos y necesitas un flag especial.

```git
git diff --staged
```

Archivos abajo ¯\\\_(ツ)\_/¯ (si, se que esto es una funcionalidad, no un error, pero es desconcertante y poco obvio la primera vez que te sucede!)

## Oh shit, necesito deshacer un commit de hace 5 comits!
```git
# encuentra el commit que necesitas deshacer
git log
# usa las flechas para moverte para arriba y abajo en la historia
# una vez que encontraste el commit, guarda su hash
git revert [hash guardado]
# git va a crear un nuevo commit que deshace ese commit
# sigue las indicaciones para editar el mensaje del commit
# o simplemente guarda y haz el commit
```

Al parecer, no necesitas buscar y copiar-pegar el contenido del viejo archivo al actual para deshacer los cambios! Si hiciste commit de un bug, puedes deshacer el commit de una con `revert`

También puedes revertir un solo archivo en vez de todo un commit! Pero, por supuesto, haciendo honor a la filosofia git, es un comando totalmente distinto.

## Oh shit, necesito deshacer los cambio de un archivo!
```git
# busca el hash del commit anterior de cuando se cambio el archivo
git log
# usa las flechas para moverte para arriba y abajo en la historia
# una vez que encontraste el commit, guarda su hash
git checkout [hash guardado] -- path/to/file
# la version anterior del archivo estará en tu index
git commit -m "Waw, no tienes que hacer copiar-pegar para deshacer"
```

Cuando me di cuenta de esto fue INCREIBLE. INCREBILE. IN-CRE-I-BLE. Pero en serio, en que planeta de mierda `checkout --` hace sentido que sea la mejor manera de deshacer un archivo? :shakes-fist-at-linus-torvalds:

## A la mierda este ruido, me doy por vencido.
```git
cd ..
sudo rm -r fucking-git-repo-dir
git clone https://some.github.url/fucking-git-repo-dir.git
cd fucking-git-repo-dir
```

Gracias a Eric V. por esta. Todas las quejas por el uso de `sudo` en este chiste pueden ser dirigidas a él.

En serio, si tu rama está tan rota que necesitas reiniciar el estado de tu repo al mismo que el repo remoto en una manera aprobada por git, prueba esto, pero ten en cuenta que son acciones destructivas e irrecuperables!

```git
# recupera el último estado del origen
git fetch origin
git checkout master
git reset --hard origin/master
# elimina los archivos y directorios sin seguimiento
git clean -d --force
# repite checkout/reset/clean para cada rama rota
```

\*Descargo: Este sitio no está pensado para ser una referencia exhaustiva. Y sí, hay otras maneras de hacer las mismas cosas de una forma teóricamente más puras, pero yo llegué a estos pasos por prueba y error y muchas puteadas, y tuve esta loca idea de compartirlas con una sana dosis de insultos. Tómalo o déjalo, como quieras!

Muchas gracias a todos los que voluntarios que tradujeron este sitio a otros idiomas, la rompen! [Michael Botha](https://github.com/michaeljabotha) ([af](https://ohshitgit.com/af)) · [Khaja Md Sher E Alam](https://github.com/sheralam) ([bn](https://ohshitgit.com/bn)) · [Eduard Tomek](https://github.com/edee111) ([cs](https://ohshitgit.com/cs)) · [Moritz Stückler](https://github.com/pReya) ([de](https://ohshitgit.com/de)) · [Franco Fantini](https://github.com/francofantini) ([es](https://ohshitgit.com/es)) · [Hamid Moheb](https://github.com/hamidmoheb1) ([fa](https://ohshitgit.com/fa)) · [Senja Jarva](https://github.com/sjarva) ([fi](https://ohshitgit.com/fi)) · [Michel](https://github.com/michelc) ([fr](https://ohshitgit.com/fr)) · [Alex Tzimas](https://github.com/Tzal3x) ([gr](https://ohshitgit.com/gr)) · [Elad Leev](https://github.com/eladleev) ([he](https://ohshitgit.com/he)) · [Aryan Sarkar](https://github.com/aryansarkar13) ([hi](https://ohshitgit.com/hi)) · [Ricky Gultom](https://github.com/quellcrist-falconer) ([id](https://ohshitgit.com/id)) · [fedemcmac](https://github.com/fedemcmac) ([it](https://ohshitgit.com/it)) · [Meiko Hori](https://github.com/meih) ([ja](https://ohshitgit.com/ja)) · [Zhunisali Shanabek](https://github.com/zshanabek) ([kk](https://ohshitgit.com/kk)) · [Gyeongjae Choi](https://github.com/ryanking13) ([ko](https://ohshitgit.com/ko)) · [Rahul Dahal](https://github.com/rahuldahal) ([ne](https://ohshitgit.com/ne)) · [Martijn ten Heuvel](https://github.com/MartijntenHeuvel) ([nl](https://ohshitgit.com/nl)) · [Łukasz Wójcik](https://github.com/lwojcik) ([pl](https://ohshitgit.com/pl)) · [Davi Alexandre](https://github.com/davialexandre) ([pt\_BR](https://ohshitgit.com/pt_BR)) · [Catalina Focsa](https://github.com/catalinafox) ([ro](https://ohshitgit.com/ro)) · [Daniil Golubev](https://github.com/dadyarri) ([ru](https://ohshitgit.com/ru)) · [Nemanja Vasić](https://github.com/GoodbyePlanet) ([sr](https://ohshitgit.com/sr)) · [Björn Söderqvist](https://github.com/cybear) ([sv](https://ohshitgit.com/sv)) · [Kitt Tientanopajai](https://github.com/kitt-tientanopajai) ([th](https://ohshitgit.com/th)) · [Taha Paksu](https://github.com/tpaksu) ([tr](https://ohshitgit.com/tr)) · [Andriy Sultanov](https://github.com/LastGenius-edu) ([ua](https://ohshitgit.com/ua)) · [Tao Jiayuan](https://github.com/taojy123) ([zh](https://ohshitgit.com/zh)) . Con la ayuda adicional de [Allie Jones](https://github.com/alliejones) · [Artem Vorotnikov](https://github.com/vorot93) · [David Fyffe](https://github.com/davidfyffe) · [Frank Taillandier](https://github.com/DirtyF) · [Iain Murray](https://github.com/imurray) · [Lucas Larson](https://github.com/LucasLarson) · [Myrzabek Azil](https://github.com/mvrzvbvk)

Si quieres ayudar a traducir a otros idiomas, envia tu PR a [GitHub](https://github.com/ksylor/ohshitgit)