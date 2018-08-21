# Autoscaling Deployments Steps - William Lee:

(Example: autoscale translation service)
1. cd /home/clipu/c2git/c2svc/build/src/staging/translation

2. Build translation:
	* `kubectl --kubeconfig=/root/.kube/config --namespace=backend create -f translation.yaml`

3. Create metrics server:
	* `kubectl --kubeconfig=/root/.kube/config --namespace=kube-system create -f v1.8.x.yaml`

	* It may take a few minutes for the metrics server to get metrics from the pods. To check metric-server status:
		* `kubectl --kubeconfig=/root/.kube/config --namespace=kube-system logs <metric-server name>`
		* Where `<metric-server name>` is replaced by getting the name of the metric-server pod
	* You can get the metric-server pod by listing `kubectl --kubeconfig=/root/.kube/config --namespace=kube-system get pods`

4. Create horizontal pod autoscaler (hpa):
	* `kubectl --kubeconfig=/root/.kube/config --namespace=backend create -f translate-autoscale.yaml`

5. Test:
	* Make sure on the k8s staging dahboard, there is an attached horizontal autoscaler for the translation deployment.
