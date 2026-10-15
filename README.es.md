# kubectl Cheatsheet · Hoja de referencia de comandos kubectl

> 🌍 [中文](README.md) · [Português](README.pt.md)

Una **hoja de referencia de una sola página** con comandos de kubectl: 30 entradas de uso diario para ver el estado, depurar, desplegar y publicar en Kubernetes. Cada entrada responde solo tres preguntas: **qué hace, un comando listo para copiar y pegar, y etiquetas de uso**. Sin parámetros inventados.

## Para quién es

Ingenieros SRE y de operaciones, desarrolladores backend y cualquiera que ejecute aplicaciones en Kubernetes. Si cada vez que un Pod se cae tienes que buscar cómo ver los logs del contenedor anterior, esta hoja es para ti.

## Cómo usarla

1. Ve directo a **[CHEATSHEET.md](CHEATSHEET.md)**: el cuerpo de la referencia; los comandos en inglés los entiende cualquier desarrollador.
2. Necesitas un clúster para practicar: minikube o kind en local, o un K8s gestionado en la nube. Si `kubectl cluster-info` devuelve una dirección, estás conectado.
3. Sigue el orden de la hoja —estado y depuración → despliegue y publicación → logs y acceso al contenedor → gestión de recursos → contextos y namespaces → herramientas de depuración— y prueba cada comando a mano. Casi todo actúa sobre el namespace actual; añade `-n <ns>` para otro.

## Pruébalo en 30 segundos

```bash
kubectl create deployment hello --image=nginx:1.27   # levanta un nginx
kubectl get pods                                     # si dice Running, funciona
kubectl delete deployment hello                      # bórralo al terminar
```

## Qué incluye

| Categoría | Contenido |
|---|---|
| 🔍 Estado y depuración | cluster-info / get nodes / get pods -A / describe / events / top (6) |
| 🚀 Despliegue y publicación | apply -f / create deployment / scale / set image / rollout restart·status·history·undo / expose (7) |
| 📜 Logs y acceso al contenedor | logs / logs -f / logs -p / exec -it / cp (5) |
| 🧰 Gestión de recursos | get combinado / edit / delete / label / port-forward (5) |
| 🧭 Contextos y namespaces | config get-contexts / use-context / get·create ns / set-context para fijar el namespace (4) |
| 🩺 Herramientas de depuración | debug con contenedor efímero / explain / diff (3) |

La documentación oficial es solo https://kubernetes.io/docs/reference/kubectl/; cada comando está verificado contra la referencia oficial de kubectl.

## Contribuciones bienvenidas

¿Un comando incorrecto, un parámetro desactualizado o una traducción mejorable? Los *pull requests* son bienvenidos. Mantén el formato (descripción / bloque bash / etiquetas) y **solo comandos reales y verificados; ante la duda, mejor no incluirlo**.

## 📚 Más hojas de referencia

Otras hojas del mismo autor, también en 中文 / Español / Português:

- [Hoja de FFmpeg](https://github.com/Ezra-Zhao/ffmpeg-cheatsheet) — 28 comandos de audio y vídeo
- [Hoja de Docker](https://github.com/Ezra-Zhao/docker-cheatsheet) — 28 comandos de docker / compose
- [Hoja de Git](https://github.com/Ezra-Zhao/git-cheatsheet) — 30 comandos diarios y de rescate
- [Hoja de curl](https://github.com/Ezra-Zhao/curl-cheatsheet) — 29 comandos para depurar APIs
- [Hoja de expresiones regulares](https://github.com/Ezra-Zhao/regex-cheatsheet) — 30 patrones prácticos
- [Hoja de jq](https://github.com/Ezra-Zhao/jq-cheatsheet) — 30 filtros para JSON
- [Hoja de terminal](https://github.com/Ezra-Zhao/terminal-superpowers-cheatsheet) — 14 herramientas de productividad
- [Hoja de alternativas a Adobe](https://github.com/Ezra-Zhao/adobe-free-alternatives-cheatsheet) — 16 alternativas gratuitas
- [Hoja para cancelar suscripciones](https://github.com/Ezra-Zhao/desubscribe-cheatsheet) — 10 cambios que ahorran ≈ $1,260/año
- [Hoja de SQL](https://github.com/Ezra-Zhao/sql-cheatsheet) — consultas, joins, agregaciones y casos prácticos
- [Hoja de SSH](https://github.com/Ezra-Zhao/ssh-cheatsheet) — conexiones, túneles y servidores bastión

## Licencia

MIT © 2026 Guangyi Zhao. Ver [LICENSE](LICENSE).
