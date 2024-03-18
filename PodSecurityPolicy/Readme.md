INTRODUCTION

Pod Security Admission 
- Restriction can be applied at namespace level using labels.
- Restrictions can be applied at cluster level as well using AdmissionConfigFile.
	- vi /etc/Kubernetes/manifest/kube-apiserver.yml 
	- Update --features-gates=PodSecurity=true
- Alternatively, install pod security admission webhook
- v1.23 onwards enabled by default
- For v 1.22 - enabled manually

![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/bad0ed35-6044-4509-ab5b-2107afea3270)


**1. How Admission Controller works ?**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/d2db4842-0d3f-400c-af02-e3b7ebada4d4)

**2. restriction at Namespace level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/7c4fb9bc-d38c-48a2-9850-8b7055f633fe)

**3. Pod Security Levels**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/48489314-da6d-40b4-8464-a943565e3068)

**4. Pod Security Modes**
![image](https://github.com/Ashish-Goel007/My-Private-repo/assets/35141714/c1de5c64-0008-4dab-86d8-5d334fa4979a)

**5. Pod Security Admission Steps**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/df53805e-3358-4bf4-adfe-557b39a1738f)

**6. PSA Labels - If rules are violated in below, creation will be blocked due to enforce mode.**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/b296ae09-9bd2-4e37-9546-32dc644d0347)

**7. POD Security at Namespace level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/0d7c123a-3f39-4391-9003-60f2356037c9)

**8. Pod security at cluster level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/f1d6faa2-7727-4896-92f0-d134f0989ce2)

**9. Commands**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/13c43dd8-214b-4e12-843e-b1c22c9ff6e8)

**10. Privileged Level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/6faf97d2-24cb-4955-b85b-b7b8a79ddc8b)

**11. Baseline Level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/cafd67b4-9685-4d89-b4b2-aec50601bd21)

**12. Restricted Level**
![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/bf093d67-c7e2-4734-8645-6837a9609128)



