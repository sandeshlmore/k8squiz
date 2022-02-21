# Chapter 1 Introduction

1. Which controller is responsible for scheduling a pod on a node?
    1. Kubelet
    2. ReplicaSet
    3. kube-scheduler

	Ans: 1. deployment -> replicaset ->  kube-scheduler -> kubelet 


2.  Arrange in sequence all controllers that play a role in launching a pod via a deployment?
	1. deployment -> replicaset ->  kube-scheduler -> kubelet
	2. Deployment -> kubelet
	3. Deployment -> replicaset -> pod -> scheduler

	Ans: 1. deployment -> replicaset ->  kube-scheduler -> kubelet


3. How does kuberentes API handles two concurrent writes to update a cluster object?
	1. Rejects both writes
	2. Accept first write, rejects second. Controller must retry / handle conflicts
	3. Queue the write operations - execute one after another
	4. Result of concurrent write is undeterministic

	Ans: 2. Accept first write, rejects second. Controller must retry / handle conflicts



# Chapter 2 Kubernetes API Basics

1.  Which command will you use to proxy Kubernetes APIs on local machine?

	Ans: kubectl proxy


2.  How do you get the supported API Versions on a kubernetes cluster?

	Ans: kubectl api-resources


3.  How do you get supported API Resources on a kubernetes cluster?

	Ans: kubectl api-resources


4.  Find out the GVR for Deployment.

	Ans: group: apps
		version: v1
		resource: deployments


5.  Find out GVK for Pods

	Ans: group: - (comes in core/legacy api-group)
		 version: v1
		 kind: pods


6.  Find out GVR for CronJob

	Ans: group: batch
		version: v1
		resource: cronjobs


7.  ServiceAccount is a non-namespaced resource - True / False

	Ans: False.


8.  Namespace is a ?

    1. namespaced resource
    2. non-namespaced resource
	Ans: 2. non-namespaced resource


9. Which of the following statements are true about GVK
    1. A Kind can be part of one and only one groupversion
    2. A Kind can be part of more than one groupversions simultaneously, but can only be retrieved as representation of a single groupversion for a cluster
    3. A Kind can be part of more than one groupversions simultaneously, and can be retrieved as representation of any of those groupversions for a cluster

	Ans: 3. A Kind can be part of more than one groupversions simultaneously, and can be retrieved as representation of any of those groupversions for a cluster


10. In API Server response processing, which of the following is true?
    1. Mutating webhooks come before Validating webhooks
    2. Validating Admission Webhooks come before mutating webhooks

	Ans: 1. Mutating webhooks come before Validating webhooks


11. API Server persists the state of various objects in etcd always
    1. True, API Server always uses etcd to store state
    2. False, it depends on the kubernetes distro, etcd may be replaced by other options
	
	Ans: 2. False, it depends on the kubernetes distro, etcd may be replaced by other options


## Chapter 3 Basics of client-go

1. The client-go library should be imported in the project as 
    1. github.com/kubernetes/client-go
    2. K8s.io/client-go

	Ans: 2. K8s.io/client-go


2. Which method is used to parse kubeconfig file?
    1. Clientcmd.BuildConfigFromFlags
    2. Rest.InClusterConfig

	Ans: 1. Clientcmd.BuildConfigFromFlags


3. The default wire format of client-go is 
    1. JSON
    2. Protobuf
    3. XML

	Ans: 1. JSON, 2. Protobuf


4. The TypeMeta struct contains which of the following fields (select all) : 
    1. Kind
    2. APIVersion
    3. Name
    4. UID

	Ans:  1. Kind, 2. APIVersion


5. The ObjectMeta contains resourceVersion - True / False

    Ans: True

6. The clientset returned by kubernetes.NewForConfig(config) gives access to 
    1. Only stable API groups and resources
    2. Only stable and beta versioned API groups and resources
    3. All API groups and resources
    4. All API Groups and resources defined in <text>k8s.io/api<text>, but not for custom resource definitions

	Ans: 4. All API Groups and resources defined in <text>k8s.io/api<text>, but not for custom resource definitions


7. Identify the non-long-running requests from following : 
    1. exec
    2. List
    3. Watch
    4. Port-forward
    5. Update
    6. Create
    7. Logs

	Ans: 2. List, 5. Update, 6. Create, 7. Logs


8. Non-long-running requests are bounded by 
    1. 30 sec
    2. 45 sec
    3. 60 sec
    4. 120 sec

	Ans: 3. 60 sec


9. List four reasons why Informers are preferred over Watches?
	Ans: 
        1. if we use watch in custom controllers everytime we need access to kubernetes object/resource, it will overload traffic on Kube-Api-Server due to frequent polling. Informers use local cache to avoid frequent calls to Kube Api server.
        
        2. Informers provide error handling by some in-built retry mechanism.
        
        3. Single resource can be watched by multiple controllers. Here Shared Informer     
        Factory is used so that the cache is shared among controllers.
        
        4. With Informers We can register functions to listen to ADD, Update and Delete events.


10. The mapping of GVK to GVR is called :
    1. RESTMapping
    2. Scheme

	Ans: 1. RESTMapping


11. By conventions, kinds are :
    1. Formatted in lowercase, and usually singular
    2. Formatted in CamelCase and usually singular
    3. Formatted in lowercase, and usually plural
    4. Formatted in CamelCase and usually plural

	Ans: 2. Formatted in CamelCase and usually singular


12. By convention, resources are :
    1. Formatted in lowercase, and usually singular
    2. Formatted in CamelCase and usually singular
    3. Formatted in lowercase, and usually plural
    4. Formatted in CamelCase and usually plural

	Ans: 3. Formatted in lowercase, and usually plural


13. Kinds map to ……… and resources map to …….
    1. Go types, REST Endpoints
    2. REST Endpoints, Go types

	Ans: 1. Go types, REST Endpoints


14. Which of the following is not a Kind:
    1. Pod
    2. Deployment
    3. services
    4. Status

	Ans: 4. Status



# Chapter 4 Using Custom Resources

1. CRDs are kuberentes resources in 
    1. apps/v1
    2. extensions/v1beta1
    3. apiextensions.k8s.io/v1beta1

    Ans: 3. apiextensions.k8s.io/v1beta1

2. For a custom resource kind "step", what will be default listKind?
    1. steps
    2. listSteps
    3. stepList

    Ans: 3. stepList


3. Select all subresources supported by Custom resources :
    1. logs
    2. status
    3. exec
    4. scale

    Ans: 2. status, 4. scale


4. Define a custom resource YAML with following validations :
    1. Spec must contain image, owner and locale fields
    2. Locale must be one of EN, DE
    3. owner must start with "org.io/"
    4. image must contain the tag and it should not be "latest"

    Ans: 


5. How does the scale subresource identify the json path for replicas?
    1. It's always .spec.replicas
    2. It's defined in Scale kind from autoscaling/v1 API group
    3. Replica json path needs to be defined in CRD

    Ans: 2. It's defined in Scale kind from autoscaling/v1 API group


6. Scale subresource can change
    1. only status & replicas of the resources
    2. only replicas of the resources
    3. status, lables and replicas of the resoureces

    Ans: 1. only status & replicas of the resources


7. Identify a typed client from the following:
    1. client-go
    2. controller-runtime

    Ans: 2. controller-runtime


8. For typed client, the processed types must be known at complie time
    1. true
    2. false

    Ans: 1. true


9. Select valid constraints when using dynamic clients :
    1. GVKs must be known at complile time
    2. RESTMapper is not used, so developer needs to provide GVR
    3. It only uses unstructured.Unstructured go type

    Ans: 2. RESTMapper is not used, so developer needs to provide GVR
         3. It only uses unstructured.Unstructured go type


10. For a custom resource, "step" with group infracloud.io, and version v1beta1, the Go types are traditionally defined in 
    1. types.go in pkg/apis/group/version
    2. types.go in pkg/apis/infracloud.io/v1beta1

    Ans: 2. types.go in pkg/apis/infracloud.io/v1beta1


## Chapter 5 Automating Code Generation

1. Which code-generators will you use for kubernetes controllers
    1. vendor/k8s.io/code-generator
    2. github.com/kubernetes/code-generator

    Ans: 1. vendor/k8s.io/code-generator


2. Global tags are written into 
    1. package's `doc.go`
    2. package's `type.go`
    3. kubeconfig file

    Ans: 1. package's `doc.go`


3. first-comment-block is 
    1. directly above the type / package line
    2. separated from the type / package line by atleast one empty line

    Ans: 1. directly above the type / package line


4. For content to show up in API HTML documentation 
    1. It must be added to second-comment-block
    2. It must be added to first-comment-block

    Ans: 2. It must be added to first-comment-block


5. `+groupName` tag is 
    1. Optional, only added for information purpose
    2. Mandatory, defines the fully qualified group name
    3. Optional, only needed if Go parent package name doesn't match group name

    Ans: 3. Optional, only needed if Go parent package name doesn't match group name


6. Tags are generally added to 
    1. second comment block so that those can be added to API documentation
    2. first comment block so that those are added to API documentation
    3. second comment block so that those can be skipped from API documentation

    Ans: 3. second comment block so that those can be skipped from API documentation


7. For `+genclient` tag, default is to
    1. generate a namespaced client
    2. generate a non-namespaced client
    3. No default, it must be specified whether the resource is namespaced / non-namespaced

    Ans: 1. generate a namespaced client


8. `+genclient` must be added to type and List type of API Object
    1. true
    2. false

    Ans: 2. false


9. Let's say we don't want spec / status split for our CR. To achieve this
    1. We need to add `+genclient` tag which will by default not generate a updateStatus method
    2. we need to add `+genclient:nostatus` so that the updateStatus method is not generated
    3. we need to add `genclient: skipVerbs=status` tag

    Ans: 2. we need to add `+genclient:nostatus` so that the updateStatus method is not generated


# Chapter 8 Custom API Servers

1. Select all RBAC permissions that are needed for the custom API Server service account?
    1. get, list, watch namespaces
    2. get, list, watch pods
    3. get, list, watch validatingwebhookconfigurations
    4. get, list, watch mutatingwebhookconfigurations
    5. create pods
    6. delete pods

    Ans: 1. get, list, watch namespaces
         3. get, list, watch validatingwebhookconfigurations
         4. get, list, watch mutatingwebhookconfigurations


2. CRDs support Protobuf and JSON
    1. True
    2. False

    Ans: 2. False


3. List down advantages of Custom API Servers over CRDs

    Ans:Custom API Servers :
         1. Can use any storage medium.
         2. Can provide protobuf support like all native Kubernetes resources do.
         3. Can implement all operations like validation, admission, and conversion reducing latency.
         4. Can implement graceful deletion.
         5. highly customizable


4. What are some key reasons you would choose CRDs over custom API Servers?

    Ans: 1. purely declarative.
         2. dont need another api server.
         3. overall less complex than witing custom api servers with golang.


5. How does `kube-aggregator` know which resources are served by a custom API Server?
    1. It queries custom API Servers
    2. Resources served by custom API Servers are registered with kube-apiserver
    3. Using APIService objects which list the API Groups and Versions

    Ans: 3. Using APIService objects which list the API Groups and Versions


6. The `service` in APIService object must serve port 443 and cannot use any other port
    1. True
    2. False

    Ans: 1. True


7. Let's say I have a group `citadel.infracloud.io` with three versions values as follows. What is the overall GroupPriority for the group `citadel.infracloud.io`
    - `citadel.infracloud.io\v1 : GroupPriorityMinimum: 1000`
    - `citadel.infracloud.io\v1 : GroupPriorityMinimum: 900`
    - `citadel.infracloud.io\v1 : GroupPriorityMinimum: 1100`
    1. 1000
    2. 900
    3. 1100

    Ans: 3. 1100


8. Custom API Servers authorize requests by (choose multiple if valid) :
    1. Delegating to kube-apiserver via TokenAccessReviews
    2. Delegating to kube-apiserver via SubjectAccessReviews
    3. Through authorization chain in Custom API Server
    4. Requests are pre-authorized by kube-apiserver authorization module
    5. Authorization cache in Custom API Server

    Ans:    2. Delegating to kube-apiserver via SubjectAccessReviews
            3. Through authorization chain in Custom API Server
            5. Authorization cache in Custom API Server


9. The API business logic is implemented :
    1. For each external version
    2. Only once for internal version
    3. Only for most recent external API Version

    Ans: 3. Only for most recent external API Version


10. For an API Server serving single API Group with 2 versions (v1alpha1 & v1beta1) and 1 validating webhook, how many conversions are carried out between internal and external versions for a single create / update request?
    1. 4
    2. 6
    3. 2 (only for v1alpha1, v1beta1 is same as internal since its the latest version — so no conversion needed)
    4. 2 (only once from external to internal version and vice-versa. All API logic & storage is then in internal version )

    Ans: 1. 4



11. For the example in above question, how many times `Defaulting` takes place for a create / update request?
    1. 1
    2. 2
    3. 4
    4. 6

    Ans: 2. 2


12. What are the differences between types.go for internal and external types? (Select All)
    1. JSON & protobuf tags are missing from external types.go
    2. JSON & protobuf tags are missing from internal types.go
    3. types.go for internal versions is in `pkg/apis/group-name/types.go` and for external versions in `pkg/apis/group-name/version/types.go`
    4. Latest API version is same as internal version

    Ans: 2. JSON & protobuf tags are missing from internal types.go
         3. types.go for internal versions is in `pkg/apis/group-name/types.go` and for external versions in `pkg/apis/group-name/version/types.go`


13. Modify the Pizza example API server in the Programming Kubernetes book for the following :
    1. Add a new version `v2alpha1`
    2. In this version, add a new field `size` with options `Small`, `Medium`, `Large`
    3. Add a validation to ensure the `size` value is one of the allowed values
    4. Default the `size` to `Medium`
    5. Implement validating admission plugin to reject the request if another pizza of same size is already available in a given namespace

    Ans:  repo link: https://github.com/sandeshlmore/pizzaserver



# Chapter 9 Advanced Custom Resources

1. For a CRD `Pizza`, following versions are defined : `v1`, `v1alpha1`, `v1beta1`, `v2experimental`. For a request `kubectl get Pizza` which version will be returned?
    1. v1beta1
    2. v2experimental
    3. v1
    4. v1alpha1

    Ans: 3. v1


2. How do you specify the versions supported by a conversion webhook?
    1. version is specified in the endpoint e.g. `/convert/v1beta1/pizza`, `/convert/v1alpha1/pizza` etc
    2. Checked only in the `convert` function in the conversion webhook.

        ```
        if apiVersion != v1beta1.SchemeGroupVersion.String() {
            return nil, fmt.Errorf("cannot convert %s to %s",
              v1alpha1.SchemeGroupVersion, apiVersion)
        }
        ```
    3. All versions of a CRD must be supported by a conversion webhook as only one such webhook can be specified

    Ans: All versions of a CRD must be supported by a conversion webhook as only one such webhook can be specified


3. Custom Admission Webhooks can only be added for CRDs and not for native Kubernetes resources
    1. True
    2. False

    Ans: 2. False


4. The order for mutating and validating webhooks is :
    1. Validating -> Mutating
    2. Mutating -> Validating

    Ans: 2. Mutating -> Validating


5. Kubernetes API Server calls
    1. Mutating webhooks parallely, validating webhooks sequentially
    2. Mutating webhooks sequentially, validating webhooks sequentially
    3. Mutating webhooks sequentially, validating webhooks parallely

    Ans: 3. Mutating webhooks sequentially, validating webhooks parallely