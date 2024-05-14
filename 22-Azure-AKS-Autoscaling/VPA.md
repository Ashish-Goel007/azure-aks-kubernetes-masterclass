To set up a Vertical Pod Autoscaler (VPA) in Kubernetes, you need to have the VPA component installed in your cluster. 
The VPA provides recommendations for the optimal resource limits (CPU and memory) for the pods 
and can also automatically apply these recommendations. Below is a sample YAML manifest for a Vertical Pod Autoscaler that targets
a specific deployment.

VPA also uses the metrics server to capture CPU in a similar way as HPA.

![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/12449273-6d17-42de-bee0-6a436eec30eb)


Update Mode
Auto - Apply the recommendaations suggested by VPA directly by updating the pods. (pods will be restarted)
Off - VPA gives the recommendations but wont update the replicas (preferred in prod since pods are not restarted in this case)
Initial - It applies the recommended values only to the newly created pods.

**Sample VPA Manifest**
Here's a simple example of a VPA configuration that automatically adjusts CPU and memory requests for the pods managed by a deployment named **example-deployment**:

        apiVersion: autoscaling.k8s.io/v1
        kind: VerticalPodAutoscaler
        metadata:
          name: example-vpa
          namespace: default
        spec:
          targetRef:
            apiVersion: "apps/v1"
            kind: Deployment
            name: example-deployment
          updatePolicy:
            updateMode: "Auto" 
          resourcePolicy:
            containerPolicies:
              - containerName: '*'
                minAllowed:
                  cpu: "100m"
                  memory: "50Mi"
                maxAllowed:
                  cpu: "1000m"
                  memory: "1024Mi"
                controlledResources: ["cpu", "memory"]


**Explanation of the Manifest Fields**
**apiVersion**: Specifies the API version for the VPA. For VPA, it's typically autoscaling.k8s.io/v1.

**kind**: Specifies the kind of the Kubernetes object; in this case, it's VerticalPodAutoscaler.

**metadata**: Contains metadata about the VPA object, such as name and namespace.

**spec**: The specification of the VPA:

  **targetRef**: References the Kubernetes object you want to autoscale. It includes the API version, the kind (like Deployment, StatefulSet), and the name of the object.
  
  **updatePolicy**: Specifies how the VPA should apply the resource requirement recommendations. Auto mode means it will automatically update the pod's resource requests as needed.

**resourcePolicy**: Defines the resource policy constraints:

  **containerPolicies**: List of policies applicable to specific containers or all containers ('*').
  
  **minAllowed and maxAllowed**: Define the minimum and maximum resource limits for CPU and memory.
  
  **controlledResources**: Specifies which resources (CPU and/or memory) are controlled by VPA.

**Steps to Apply This Manifest**

1. **Ensure VPA is Installed**: Before applying the manifest, make sure that the VPA admission controller is installed in your cluster. This component is necessary for the VPA to function.
2. **Apply the Manifest**: Use kubectl to apply this YAML file to your Kubernetes cluster:

kubectl apply -f vpa.yaml

3. **Monitor the VPA**: After applying, you can monitor the VPA's recommendations and actions using:
   kubectl get vpa example-vpa -o yaml

This YAML setup instructs the VPA to automatically manage the CPU and memory resources within specified limits, optimizing your application's performance and resource usage based on its actual needs.
