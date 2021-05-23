# Build-and-Deploy-a-Docker-Image-to-a-Kubernetes-Cluster



mkdir echo-web

gsutil cp gs://sureskills-ql/challenge-labs/ch04-kubernetes-app-deployment/echo-web.tar.gz .

tar -xzf echo-web.tar.gz

rm echo-web.tar.gz

docker build -t echo-app:v1 .

docker tag echo-app:v1 gcr.io/$DEVSHELL_PROJECT_ID/echo-app:v1

docker push gcr.io/$DECSHELL_PROJECT_ID/echo-app:v1

gcloud builds submit --tag gcr.io/$DEVSHELL_PROJECT_ID/echo-app:v1  .

gcloud config set compute/zone us-central1-a

gcloud container clusters create echo-cluster  --num-nodes=2 --machine-type=n1-standard-2

kubectl create deployment echo-web --image=gcr.io/qwiklabs-resources/echo-app:v1

kubectl expose deployment echo-web --type=LoadBalancer --port=80 --target-port=8000


kubectl get svc # wait until external ip show


copy all code to your CLI
