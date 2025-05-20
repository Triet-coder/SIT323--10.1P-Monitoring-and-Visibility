1. Made a basic Node.js application with Express that says "Hello, GCP Kubernetes!" when it listens on port 3000.
2. Docker was used to containerize the application by creating a Dockerfile, then locally building and testing the image.
3. Used the following to push the Docker image to the Google Container Registry (GCR):
- docker build -t gcr.io/my-project-sit323/node-app:v1 .
- docker push gcr.io/my-project-sit323/node-app:v1
4. Created a Kubernetes Cluster using:
- gcloud container clusters create node-cluster --zone us-central1-a --num-nodes 1
- gcloud container clusters get-credentials node-cluster --zone us-central1-a
5.  Deployed the App to GKE using deployment.yaml and service.yaml. The service was of type LoadBalancer to expose the app to the internet.
6.  Verified the Deployment by retrieving the external IP using:
- kubectl get services

Tools and Configurations Used
Cloud-native tools and a variety of GCP services were used in the project. The Docker image was stored in the Google Container Registry, and the infrastructure was hosted on Google Cloud Platform. The Kubernetes cluster was managed by GKE, and cluster interaction was handled by kubectl. Cloud Logging and Cloud Monitoring (formerly Stackdriver) were used to keep an eye on the application. Logs Explorer's logging filters were configured to view container logs in real time, and monitoring dashboards such as "Autoscaler Monitoring" and "Cluster Health Scanner" offered insight into performance and resource utilization. I was able to observe the application layer as well as the infrastructure thanks to these tools.

Issues and Challenges Faced
During the deployment, a number of difficulties surfaced. The Artifact Registry API was initially disabled, which prevented me from pushing the Docker image to GCR. I fixed this by turning it on in the GCP Console. Additionally, I came across a billing restriction that required me to link a billing account, even though the free trial prevented charges from being applied. The missing gke-gcloud-auth-plugin was another problem, which I fixed by installing it using the CLI. Furthermore, it took a while for the service's external IP to show up because of provisioning delays, and the logs weren't visible in the Logs Explorer until I accessed the app to initiate activity.
