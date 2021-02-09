# GitOpsTalk
Talk about GitOps with argoCD

## Prerequisitos

Para la demo vamos a usar una instancia de minikube para la instalación y configuración de ArgoCD

Y para el despliegue de la aplicación se puede generar en el mismo cluster de minikube y/o usar algun otro dependiendo del tiempo.

## Instalación de ArgoCD

La instalación es bastante sencilla, basta con crear el namespace de argocd y aplicar los manifest de la última versión disponible de Argo:

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Espera a que los componentes de ArgoCD estén arriba, una vez con los componentes corriendo habilita el portforward para poder acceder a la interfaz web.

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

El usuario por default es admin y la contraseña es el nombre del pod argocd-server

```sh
kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```

Por default argo va a configurar el mismo cluster donde corre como cluster disponible para correr las cargas, podemos levantar una aplicación demo para ver como se genera desde el CLI.

Repo:       https://github.com/argoproj/argocd-example-apps.git
Path:       guestbook
Namespace:  default

Para ver la aplicación corriendo:

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```


## Referencias

[ArgoCD](https://argoproj.github.io/argo-cd/)