## organizar.sh

```

#!/bin/bash

cd /workspace/atividades/2-desafio-arquivos

for arquivo in *; do
	if [ -f "$arquivo" ]; then
		extensao="${arquivo##*.}"
		pasta="${extensao^^}s"
		mkdir -p "$pasta"
		mv "$arquivo" "$pasta/"
	fi	
done

```

## vigiar.sh

```
#!/bin/bash

pasta=/workspace/atividades/2-desafio-arquivos/
/workspace/atividades/2-desafio-arquivos/scripts/organizar.sh

echo "Vigiando a pasta $pasta (pressione contrl+C para sair)"

inotifywait -m -e create -e moved_from "$pasta" |
	while read evento; do
		echo "Evento: $evento"
		/workspace/atividades/2-desafio-arquivos/scripts/organizar.sh
	done

```
