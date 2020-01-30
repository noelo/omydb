# resourcegate

OpenShift resource linter - enforce consistency on k8s/OCP resources

* Are health check and readiness probes declared
* Validate counts and timeouts for probes - Ensure liveness & readiness probes times/timeouts are not too short
* Deployment replica count is > 1
* Are the two health checks pointing to the same endpoint (antipattern)
* Are there limits assigned to the pods (memory, cpu, others), are those limits too large ?
* Are there prescriptive labels assigned
* Is the service account defined ?
* Is there annotations for driving prometheus metrics scraping
* Is the java XMS XMX settings greater than the pod limits
* Are secrets in a consistent place on the pod FS
* Warn if are secrets mounted as environment variables.
* Are services exposed on consistent ports
* Volumes not defined or defined and not mounted
* Warnings on pulling latest image
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



https://blog.openshift.com/fine-grained-policy-enforcement-in-openshift-with-open-policy-agent/

https://blog.colinbreck.com/kubernetes-liveness-and-readiness-probes-how-to-avoid-shooting-yourself-in-the-foot/

https://github.com/instrumenta/conftest

https://learnk8s.io/production-best-practices


