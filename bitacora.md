# Bitácora del laboratorio de rescate.

¿qué muestra cada comando?
git log->Muestra todos los commits hechos con cada detalle y en orden del mas receiente al mas antiguo
git log --oneline->Muestra los commits en una sola linea cada uno, acortando su hash y mensaje
git log --oneline --graph --all-> Muestra los commits reducidos, dando un grafico en la termina de como estan los branches y ramas incluyendo todo el historial

¿Qué es el código que aparece al inicio de cada commit?
Es el hash unico de cada commit, es decir el identificador unico de cada commit

¿por qué el segundo git diff no mostró nada?
Por que git diff es para reportar o visualizar que cambios no se han agregado, al hacer git add se empaquetaron los cambios y ya no quedaron pendientes, al hacer denuevo el git diff no muestra nada por que no hay nada pendiente

¿Qué muestra --staged?
Muestra los cambios ya agregados, osea empaquetados, este muestra a los cambios que ya se agregaron con git add

¿qué hace git restore?
Restablece los cambios que se han hecho antes de hacer un commit descartando los cambios no confirmados ni guardados

¿Funcionaría si nunca hubieras hecho commit de ese archivo?
No, si no hubiera un historial de lo que se habia guardado, git no tiene de donde restablecer cambios, entonces no funcionaria 

¿qué diferencia hay entre git restore y git restore --staged?
• git restore: descarta los cambios que se hicieron y lo devuelve a como estaba en el último commit
• git restore --staged: saca el archivo del área de preparación, deshaciendo un git add.

¿git revert borró el commit equivocado o creó uno nuevo? ¿Por qué es la opción segura cuando ya se hizo push?
git revert creó un commit nuevo; no borró el commit equivocado. Ese commit nuevo aplica los cambios inversos para anular el efecto del anterior.

¿Por qué es la opción segura tras hacer push?

• No reescribe el historial: el commit original sigue existiendo en el registro, así que no alteras la historia compartida.
• Evita git push --force: al avanzar con un commit normal, subes los cambios con un git push estándar sin pisar el trabajo de otras personas.
• Previene conflictos en el equipo: si otros compañeros ya descargaron o trabajan sobre ese commit, no tendrán historiales divergentes ni errores complejos al hacer pull o merge.
• Deja trazabilidad clara: queda documentado qué cambio causó el problema y cuál lo revirtió, lo que facilita auditorías y revisiones

¿qué diferencia hay entre git reset --soft y git revert? ¿Cuándo se usa cada uno?
 La diferencia clave es que git reset --soft retrocede el puntero de tu rama y reescribe el historial local, mientras que git revert avanza el historial creando un commit nuevo que deshace cambios anteriores sin borrar nada.

Comparativa rápida


Característica	git reset --soft	git revert
Historial de commits	Borra los commits posteriores al punto elegido	Conserva todos los commits intactos
Commits nuevos	No crea commits	Crea un commit inverso nuevo
Tus archivos	Mantiene los cambios en el área de preparación (staging)	Aplica el cambio inverso en los archivos
Uso tras git push	Peligroso (requiere push --force)	Seguro (funciona con push normal)


¿Cuándo usar git reset --soft?

Úsalo solo en commits locales que aún no has subido al repositorio remoto (push) o en una rama privada donde nadie más trabaja:
• Corregir un commit reciente: te equivocaste en el mensaje o olvidaste incluir un archivo; retrocedes con git reset --soft HEAD~1, haces los ajustes y vuelves a hacer commit.
• Agrupar varios commits pequeños (squash): si hiciste tres commits seguidos en local y quieres unirlos en uno solo más limpio antes de compartir tu rama.

¿Cuándo usar git revert?

Úsalo siempre que los cambios ya sean públicos o compartidos con tu equipo:
• Ya hiciste git push: necesitas deshacer un error en main, develop o una rama compartida sin romper el historial de tus compañeros.
• Deshacer un commit antiguo: quieres anular los cambios de un commit específico que quedó en medio del historial sin borrar los commits que se hicieron después.

¿para qué sirve git stash? ¿Qué hace git stash pop?

git stash guarda temporalmente los cambios que aún no has confirmado (commit) para dejar tu directorio de trabajo limpio, y git stash pop recupera esos cambios guardados y los elimina de la pila temporal.

¿Para qué sirve git stash?

Funciona como un cajón temporal donde guardas tu trabajo a medias cuando necesitas pausar lo que estás haciendo sin crear un commit incompleto:
• Cambiar de rama rápido: si estás trabajando en una funcionalidad y surge un error urgente en otra rama, haces git stash para poder hacer git switch o git checkout sin que Git te bloquee por tener archivos sin guardar.
• Actualizar tu rama: antes de hacer git pull, puedes guardar tus cambios locales para evitar conflictos inmediatos.
• Probar algo desde cero: te permite volver temporalmente al estado del último commit limpio para hacer una prueba y luego recuperar tu avance.

¿Qué hace git stash pop?

Cuando vuelves a la rama donde estabas trabajando y ejecutas git stash pop, ocurren dos cosas al mismo tiempo:
1. Aplica los cambios: vuelve a poner en tus archivos las modificaciones más recientes que habías guardado.
2. Borra el registro del stash: elimina ese guardado de la lista de stashes (a diferencia de git stash apply, que recupera los cambios pero deja una copia guardada).

$ git log --oneline --graph
* 3ee22bc (HEAD -> main, origin/main, origin/HEAD) docs: completa bitácora del laboratorio
* 0ae16e8 docs: agrega línea 5 a notas
* 7fdd417 (fix/urgente) feat: agrega borrador completo
* d0a7398 docs: Bitacora
* bfd18ce fix: limpia notas
* eecae20 docs: agrega línea 4 a notas
* 9aec04e chore: agrega .gitignore para archivos .env
* ab81acb feat: agrega notas y bitacora
* c22119d Initial commit


