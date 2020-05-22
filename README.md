# OMYDB

OpenShift resource linter - enforce consistency on k8s/OCP resources

Intended to be used as part of a CI/CD pipeline to ensure resource consistency. 
Jenkins and Tekton need to be supported

## Policies
* Are liveness and readiness probes declared
* Are the two probe endpoints pointing to the same endpoint (antipattern)
* Validate counts and timeouts for probes - Ensure liveness & readiness probes times/timeouts are not too short
* Deployment replica count is < 1
* Are there limits assigned to the pods (memory, cpu, others), are those limits too large ? See [0]
* Are there prescriptive labels assigned
* Is the service account defined ?
* Is there annotations for driving prometheus metrics scraping
* Is the java XMS XMX settings greater than the pod limits
* Are secrets in a consistent place on the pod FS
* Warn if are secrets mounted as environment variables.
* Are services exposed on consistent ports
* Volumes not defined or defined and not mounted
* Warnings on pulling image with latest tag
* Warnings on route name definitions e.g. DNS subdomains etc
* Pull images and report on image sizes, set maximum allowed
* Warnings on OCP/K8s api versions being used
* Warnings on deprecated API resources
* Check consistency of resources e.g. using an non-default SA, where is the SA definition
* Ensuring that base images are used and up to date
* Are there pod disruption budgets used
* Service selectors match pod labels
* Check that default SA secrets are not being mounted or if so that there is a label/annotation
* Warning on pulling images directly rather than using image streams
* Warning on using DeploymentConfigs rather than Deployments if no hooks configured
* Generic warning on using OCP resources over K8s resources if not required
* Generic warning if custom SA is defined but not used in DC/Deployment
* Warning if PVC defined but not used
* Warning is resource request and limits are inverted
* Warning using local storage volumes as this will impact workload placement
* Warning using host networks
* K8s recommended labels https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/

[0] https://www.reddit.com/r/kubernetes/comments/all1vg/on_kubernetes_cpu_limits/

Potentially resource annotation can be added to enable tests to be skipped (TBD).
Definition of rules can be retrived from an endpoint e.g. http, file etc
Skopeo can be used to inspect images and perform checks on that information

## Blogs / Reading Material
- https://blog.openshift.com/fine-grained-policy-enforcement-in-openshift-with-open-policy-agent/
- https://blog.colinbreck.com/kubernetes-liveness-and-readiness-probes-how-to-avoid-shooting-yourself-in-the-foot/
- https://github.com/instrumenta/conftest
- https://learnk8s.io/production-best-practices
