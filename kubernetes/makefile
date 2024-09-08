apply-all:
	kubectl apply -f 1-namespace.yaml
	kubectl apply -f 2-secrets.yaml
	kubectl apply -f 3-db-configmap.yaml
	kubectl apply -f 3.1-db-deployment.yaml
	kubectl apply -f 3.2-db-service.yaml
	kubectl apply -f 4-app-deployment.yaml
	kubectl apply -f 4.1-app-service.yaml

delete-all:		
	kubectl delete -f 4.1-app-service.yaml
	kubectl delete -f 4-app-deployment.yaml
	kubectl delete -f 3.2-db-service.yaml
	kubectl delete -f 3.1-db-deployment.yaml
	kubectl delete -f 3-db-configmap.yaml
	kubectl delete -f 2-secrets.yaml
	kubectl delete -f 1-namespace.yaml
