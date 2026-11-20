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
No, si no hubiera un historial de lo que se habia guardado, git no tiene de donde restablecer cambios

¿qué diferencia hay entre git restore y git restore --staged?
• git restore: descarta los cambios que se hicieron y lo devuelve a como estaba en el último commit 
• git restore --staged: saca el archivo del área de preparación, deshaciendo un git add.
