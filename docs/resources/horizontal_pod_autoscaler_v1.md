---
subcategory: "autoscaling/v1"
page_title: "Kubernetes: kubernetes_horizontal_pod_autoscaler_v1"
description: |-
  Horizontal Pod Autoscaler automatically scales the number of pods in a replication controller, deployment or replica set based on observed CPU utilization.
---

# kubernetes_horizontal_pod_autoscaler_v1 

Horizontal Pod Autoscaler automatically scales the number of pods in a replication controller, deployment or replica set based on observed CPU utilization.

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `metadata` (Block List, Min: 1, Max: 1) Standard horizontal pod autoscaler's metadata. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata (see [below for nested schema](#nestedblock--metadata))
- `spec` (Block List, Min: 1, Max: 1) Behaviour of the autoscaler. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status (see [below for nested schema](#nestedblock--spec))

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--metadata"></a>
### Nested Schema for `metadata`

Optional:

- `annotations` (Map of String) An unstructured key value map stored with the horizontal pod autoscaler that may be used to store arbitrary metadata. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
- `generate_name` (String) Prefix, used by the server, to generate a unique name ONLY IF the `name` field has not been provided. This value will also be combined with a unique suffix. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#idempotency
- `labels` (Map of String) Map of string keys and values that can be used to organize and categorize (scope and select) the horizontal pod autoscaler. May match selectors of replication controllers and services. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
- `name` (String) Name of the horizontal pod autoscaler, must be unique. Cannot be updated. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names
- `namespace` (String) Namespace defines the space within which name of the horizontal pod autoscaler must be unique.

Read-Only:

- `generation` (Number) A sequence number representing a specific generation of the desired state.
- `resource_version` (String) An opaque value that represents the internal version of this horizontal pod autoscaler that can be used by clients to determine when horizontal pod autoscaler has changed. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#concurrency-control-and-consistency
- `uid` (String) The unique in time and space value for this horizontal pod autoscaler. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#uids


<a id="nestedblock--spec"></a>
### Nested Schema for `spec`

Required:

- `max_replicas` (Number) Upper limit for the number of pods that can be set by the autoscaler.
- `scale_target_ref` (Block List, Min: 1, Max: 1) Reference to scaled resource. e.g. Replication Controller (see [below for nested schema](#nestedblock--spec--scale_target_ref))

Optional:

- `min_replicas` (Number) Lower limit for the number of pods that can be set by the autoscaler, defaults to `1`.
- `target_cpu_utilization_percentage` (Number) Target average CPU utilization (represented as a percentage of requested CPU) over all the pods. If not specified the default autoscaling policy will be used.

<a id="nestedblock--spec--scale_target_ref"></a>
### Nested Schema for `spec.scale_target_ref`

Required:

- `kind` (String) Kind of the referent. e.g. `ReplicationController`. More info: http://releases.k8s.io/HEAD/docs/devel/api-conventions.md#types-kinds
- `name` (String) Name of the referent. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names

Optional:

- `api_version` (String) API version of the referent





## Example Usage

```terraform
resource "kubernetes_horizontal_pod_autoscaler_v1" "example" {
  metadata {
    name = "terraform-example"
  }

  spec {
    max_replicas = 10
    min_replicas = 8

    scale_target_ref {
      kind = "Deployment"
      name = "MyApp"
    }
  }
}
```

## Import

Horizontal Pod Autoscaler can be imported using the namespace and name, e.g.

```
$ terraform import kubernetes_horizontal_pod_autoscaler_v1.example default/terraform-example
```