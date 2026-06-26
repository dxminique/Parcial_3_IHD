Despliegue tienda-perritos en EKS (namespace 'tienda')

1) Configurar kubectl contra tu cluster:
   aws eks update-kubeconfig --region us-east-1 --name <NOMBRE_TU_CLUSTER>

2) Aplicar namespace:
   kubectl apply -f namespace.yaml

3) Aplicar recursos de base de datos:
   kubectl apply -f mysql-secret.yaml
   kubectl apply -f mysql-deployment.yaml
   kubectl apply -f mysql-service.yaml

4) Aplicar backend:
   kubectl apply -f backend-deployment.yaml
   kubectl apply -f backend-service.yaml

5) Aplicar frontend:
   kubectl apply -f frontend-deployment.yaml
   kubectl apply -f frontend-service.yaml

6) Aplicar autoscaling (HPA):
   kubectl apply -f backend-hpa.yaml
   kubectl apply -f frontend-hpa.yaml

7) Verificar:
   kubectl get pods -n tienda
   kubectl get svc tienda-frontend -n tienda
   kubectl get hpa -n tienda

Copia el EXTERNAL-IP (DNS del ELB) y abrelo en el navegador
-> deberias ver la pagina de Tienda de Perritos

Nota: Si un pod queda en estado Pending, valida la configuracion de red
(VPC, subnets, security groups) y los IAM roles del cluster/nodos.
Si un pod queda en ImagePullBackOff, valida que el account ID y la
region en la imagen del YAML coincidan con tu ECR real.
