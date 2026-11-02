A container packages an app so so runs the same anywhere, Kubernetes runs those containers as pods across a cluster of machines, and Argo CD deploys them from Git.

### Key Definitions
- **Container**: your app with everything it needs (runtime, libraries, config) packed together and will run the same on any machine. Docker builds them. An **image**(a packaged version of the application) is saved and versioned e.g. backend 2.14.0
- **Cluster**: a group of machines(nodes) managed together by Kubernetes.
- **Pod**: the smallest deployable unit in Kubernetes. Usually one pod contains one backend container. Pods are disposable. Our backend Pods are stateless, meaning they do not keep important application data locally; the data lives in external systems such as the database.
- **Deployment**: tells Kubernetes how many replicas of a Pod should be running and which version of the application they should use.
- **Service**: a stable network address in front of a set of Pods. The frontend can call something like `http://backend:8080` and the Service routes the reqeusts to an available/ready backend Pod. Pod IPs can change, but the Service address remains stable.
- **Namespace**: a logical boundary used to organise and isolate resources inside a Kubernetes cluster. For example, a cluster might have `dev`, `test`, and `prod` namespaces.
### Argo CD
Argo CD watches the Kubernetes configuration stored in Git and makes the cluster match that desired state.

Git is the source of truth: if the cluster differs from Git, Argo CD shows the application as **OutOfSync**. Syncing applies the desired configuration from Git to the cluster.

### Example on how it can be used - CI then CD
1. Merge to `dev` in GitLab -> run tests, build the application, and creates a versioned container image.
2. The deployment config is updated to reference the new image version in Git.
3. Argo CD detects the Git change and shows the application as OutOfSync.
4. Sync Argo CD -> Kubernetes creates the new Pods using the new image.

