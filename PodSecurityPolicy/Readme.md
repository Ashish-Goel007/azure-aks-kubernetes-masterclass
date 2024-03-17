Pod Security Admission 
- Restriction can be applied at namespace level using labels.
- Restrictions can be applied at cluster level as well using AdmissionConfigFile.
	- vi /etc/Kubernetes/manifest/kube-apiserver.yml 
	- Update --features-gates=PodSecurity=true
- Alternatively, install pod security admission webhook
- v1.23 onwards enabled by default
- For v 1.22 - enabled manually


Ex
apiVersion: v1
kind: Namespace
metadata:
 name: dev
 labels:
	#pod-security.kubernetes.io/<MODE> = <LEVEL>
	 pod-security.kubernetes.io/enforce: privileged

1. Pod Security Levels
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/48489314-da6d-40b4-8464-a943565e3068)


2. Pod Security Modes

 ![image](https://github.com/Ashish-Goel007/My-Private-repo/assets/35141714/c1de5c64-0008-4dab-86d8-5d334fa4979a)

