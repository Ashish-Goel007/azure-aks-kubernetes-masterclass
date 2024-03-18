WHY Pod Security Admission ?

Pod security policies can be applied on all pods in a cluster whereas 
Pod Security Admission can be applied at cluster or at namespace or pod level.

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


****************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************


The Privileged policy is purposely-open, and entirely unrestricted.

Baseline Policy - The Baseline policy is aimed at ease of adoption for common containerized workloads while preventing known privilege escalations. 
1. Windows pods offer the ability to run HostProcess containers which enables privileged access to the Windows node. Privileged access to the host is disallowed in the baseline policy.
2. Sharing the host namespaces must be disallowed.
3. Privileged Pods disable most security mechanisms and must be disallowed.
4. Adding additional capabilities beyond those listed below must be disallowed.
5. HostPath volumes must be forbidden.
6. HostPorts should be disallowed entirely (recommended) or restricted to a known list
7. On supported hosts, the runtime/default AppArmor profile is applied by default. The baseline policy should prevent overriding or disabling the default AppArmor profile, or restrict overrides to an allowed set of profiles.
8. Setting the SELinux type is restricted, and setting a custom SELinux user or role option is forbidden.
9. The default /proc masks are set up to reduce attack surface, and should be required.
10. Seccomp profile must not be explicitly set to Unconfined.
11. Sysctls can disable security mechanisms or affect all containers on a host, and should be disallowed except for an allowed "safe" subset. A sysctl is considered safe if it is namespaced in the container or the Pod, and it is isolated from other Pods or processes on the same Node.



Restricted Policy - The Restricted policy is aimed at enforcing current Pod hardening best practices, at the expense of some compatibility
1. The restricted policy only permits the following volume types.
	spec.volumes[*].configMap
	spec.volumes[*].csi
	spec.volumes[*].downwardAPI
	spec.volumes[*].emptyDir
	spec.volumes[*].ephemeral
	spec.volumes[*].persistentVolumeClaim
	spec.volumes[*].projected
	spec.volumes[*].secret
2. Containers must be required to run as non-root users.
3. Containers must not set runAsUser to 0
4. Seccomp profile must be explicitly set to one of the allowed values. Both the Unconfined profile and the absence of a profile are prohibited. This is Linux only policy in v1.25+ (spec.os.name != windows)
5. Containers must drop ALL capabilities, and are only permitted to add back the NET_BIND_SERVICE capability. This is Linux only policy in v1.25+ (.spec.os.name != "windows")
