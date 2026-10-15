# kubectl Cheatsheet · Cola de referência de comandos kubectl

> 🌍 [中文](README.md) · [Español](README.es.md)

Uma **cola de uma página só** com comandos do kubectl: 30 entradas de uso diário para ver o estado, depurar, implantar e publicar no Kubernetes. Cada entrada responde a apenas três perguntas: **o que ela faz, um comando pronto para copiar e colar, e etiquetas de uso**. Sem parâmetros inventados.

## Para quem é

Engenheiros SRE e de operações, desenvolvedores backend e qualquer pessoa que rode aplicações no Kubernetes. Se toda vez que um Pod cai você precisa pesquisar como ver os logs do contêiner anterior, esta cola é para você.

## Como usar

1. Vá direto ao **[CHEATSHEET.md](CHEATSHEET.md)**: o corpo da referência; os comandos em inglês qualquer desenvolvedor entende.
2. Você precisa de um cluster para praticar: minikube ou kind no local, ou um K8s gerenciado na nuvem. Se `kubectl cluster-info` devolver um endereço, você está conectado.
3. Siga a ordem da cola —estado e depuração → implantação e publicação → logs e acesso ao contêiner → gestão de recursos → contextos e namespaces → ferramentas de depuração— e teste cada comando na mão. Quase tudo atua no namespace atual; adicione `-n <ns>` para outro.

## Teste em 30 segundos

```bash
kubectl create deployment hello --image=nginx:1.27   # sobe um nginx
kubectl get pods                                     # se mostrar Running, funcionou
kubectl delete deployment hello                      # apague ao terminar
```

## O que está incluído

| Categoria | Conteúdo |
|---|---|
| 🔍 Estado e depuração | cluster-info / get nodes / get pods -A / describe / events / top (6) |
| 🚀 Implantação e publicação | apply -f / create deployment / scale / set image / rollout restart·status·history·undo / expose (7) |
| 📜 Logs e acesso ao contêiner | logs / logs -f / logs -p / exec -it / cp (5) |
| 🧰 Gestão de recursos | get combinado / edit / delete / label / port-forward (5) |
| 🧭 Contextos e namespaces | config get-contexts / use-context / get·create ns / set-context para fixar o namespace (4) |
| 🩺 Ferramentas de depuração | debug com contêiner efêmero / explain / diff (3) |

A documentação oficial é só https://kubernetes.io/docs/reference/kubectl/; cada comando foi verificado contra a referência oficial do kubectl.

## Contribuições são bem-vindas

Achou um comando errado, um parâmetro desatualizado ou uma tradução a melhorar? *Pull requests* são bem-vindos. Mantenha o formato (descrição / bloco bash / etiquetas) e **só comandos reais e verificados; na dúvida, melhor não incluir**.

## 📚 Mais colas de referência

Outras colas do mesmo autor, também em 中文 / Español / Português:

- [Cola de FFmpeg](https://github.com/Ezra-Zhao/ffmpeg-cheatsheet) — 28 comandos de áudio e vídeo
- [Cola de Docker](https://github.com/Ezra-Zhao/docker-cheatsheet) — 28 comandos de docker / compose
- [Cola de Git](https://github.com/Ezra-Zhao/git-cheatsheet) — 30 comandos diários e de resgate
- [Cola de curl](https://github.com/Ezra-Zhao/curl-cheatsheet) — 29 comandos para depurar APIs
- [Cola de expressões regulares](https://github.com/Ezra-Zhao/regex-cheatsheet) — 30 padrões práticos
- [Cola de jq](https://github.com/Ezra-Zhao/jq-cheatsheet) — 30 filtros para JSON
- [Cola de terminal](https://github.com/Ezra-Zhao/terminal-superpowers-cheatsheet) — 14 ferramentas de produtividade
- [Cola de alternativas ao Adobe](https://github.com/Ezra-Zhao/adobe-free-alternatives-cheatsheet) — 16 alternativas gratuitas
- [Cola para cancelar assinaturas](https://github.com/Ezra-Zhao/desubscribe-cheatsheet) — 10 trocas que economizam ≈ $1,260/ano
- [Cola de SQL](https://github.com/Ezra-Zhao/sql-cheatsheet) — consultas, joins, agregações e casos práticos
- [Cola de SSH](https://github.com/Ezra-Zhao/ssh-cheatsheet) — conexões, túneis e servidores bastião

## Licença

MIT © 2026 Guangyi Zhao. Veja [LICENSE](LICENSE).
