### Deploy

1. Ejecutar minikube con el perfil `guestbook-multinode` y con 3 nodos
```sh
minikube start -p guestbook-multinode --nodes 3
```

2. Verificar que los nodos se hayan creado correctamente
```sh
# Desde minikube
minikube status -p guestbook-multinode

# Desde kubectl
kubectl get nodes
```

3. Crear services, replication controllers y pods desde el template
```sh
kubectl create -f guestbook.yaml
```

4. Verificar que los objetos se hayan creado correctamente.
  - Los pods pueden tardar unos minutos en crearse. Verificar hasta que la columna Ready este en 1/1
  - En services notar que el External_IP de guestbook aparece como \<pending\>

```sh
# Replication Controllers
kubectl get rc

# Services
kubectl get services con labels (como app=redis, role=master)

# Pods
kubectl get pods
```

5. Exponer el puerto de guestbook al host para poder ingresar a la aplicación.
  - Abrir un tunel con minikube.
  - Correr en un terminal separado en paralelo.
```
minikube tunnel
```

6. Mientras el tunel de minikube se encuentra abierto, buscar el EXTERNAL_IP asignado a guestbook nuevamente.
```
kubectl get services
```

7. Ingresar a la IP encontrada en el paso anterior en el puerto 3000.
8. Aparece la interfaz del Guestbook.
