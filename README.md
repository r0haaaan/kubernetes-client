# Kubernetes & OpenShift Java Client [![Join the chat at https://gitter.im/fabric8io/kubernetes-client](https://badges.gitter.im/fabric8io/kubernetes-client.svg)](https://gitter.im/fabric8io/kubernetes-client?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
This client provides access to the full [Kubernetes](http://kubernetes.io/) &
[OpenShift](http://openshift.org/) REST APIs via a fluent DSL.

[![Build](https://github.com/fabric8io/kubernetes-client/workflows/Build/badge.svg)](https://github.com/fabric8io/kubernetes-client/actions?query=workflow%3ABuild)
[![Sonar Scanner](https://github.com/fabric8io/kubernetes-client/workflows/Sonar%20Scanner/badge.svg)](https://github.com/fabric8io/kubernetes-client/actions?query=workflow%3A%22Sonar+Scanner%22)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=fabric8io_kubernetes-client&metric=bugs)](https://sonarcloud.io/dashboard?id=fabric8io_kubernetes-client)
[![E2E Tests](https://github.com/fabric8io/kubernetes-client/workflows/E2E%20Tests/badge.svg)](https://github.com/fabric8io/kubernetes-client/actions?query=workflow%3A%22E2E+Tests%22)
[![Release](https://img.shields.io/github/v/release/fabric8io/kubernetes-client)](https://search.maven.org/search?q=g:io.fabric8%20a:kubernetes-client)
[![Twitter](https://img.shields.io/twitter/follow/fabric8io?style=social)](https://twitter.com/fabric8io)

| Module | Maven Central | Javadoc |
|-|:-:|:-:|
| kubernetes-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/kubernetes-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/kubernetes-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/kubernetes-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/kubernetes-client) |
| openshift-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/openshift-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/openshift-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/openshift-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/openshift-client) |

| Extensions | Maven Central | Javadoc |
|-|:-:|:-:|
| knative-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/knative-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/knative-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/knative-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/knative-client) |
| tekton-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/tekton-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/tekton-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/tekton-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/tekton-client) |
| chaosmesh-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/chaosmesh-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/chaosmesh-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/chaosmesh-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/chaosmesh-client) |
| volumesnapshot-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/volumesnapshot-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/volumesnapshot-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/volumesnapshot-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/volumesnapshot-client) |
| volcano-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/volcano-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/volcano-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/volcano-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/volcano-client) |
| istio-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/istio-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/istio-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/istio-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/istio-client) |
| open-cluster-management-client | [![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.fabric8/open-cluster-management-client/badge.svg?color=blue)](https://maven-badges.herokuapp.com/maven-central/io.fabric8/open-cluster-management-client) | [![Javadocs](https://www.javadoc.io/badge/io.fabric8/open-cluster-management-client.svg?color=blue)](https://www.javadoc.io/doc/io.fabric8/open-cluster-management-client) |

## Contents
- [Usage](#usage)
    - [Creating a client](#creating-a-client)
    - [Configuring the client](#configuring-the-client)
    - [Loading resources from external sources](#loading-resources-from-external-sources)
    - [Passing a reference of a resource to the client](#passing-a-reference-of-a-resource-to-the-client)
    - [Adapting a client](#adapting-the-client)
        - [Adapting and close](#adapting-and-close)
- [Generating CRD from Java](doc/CRD-generator.md)
- [Generating Java from CRD](doc/java-generation-from-CRD.md)
- [Mocking Kubernetes](#mocking-kubernetes)
- [Who Uses Fabric8 Kubernetes Client?](#who-uses-kubernetes--openshift-java-client)
- [Kubernetes Operators in Java Written using Fabric8 Kubernetes Client](./doc/KubernetesOperatorsInJavaWrittenUsingFabric8.md)
- [Kubernetes and Red Hat OpenShift Compatibility](#compatibility)
- [Kubernetes Client CHEAT SHEET](https://github.com/fabric8io/kubernetes-client/blob/main/doc/CHEATSHEET.md)
- [Kubectl Java Equivalents](#kubectl-java-equivalents)
- [FAQs](doc/FAQ.md) - which includes details about project dependencies.

## Usage

### Creating a client
The easiest way to create a client is:

```java
KubernetesClient client = new KubernetesClientBuilder().build();
```

`DefaultOpenShiftClient` implements both the `KubernetesClient` & `OpenShiftClient` interface so if you need the
OpenShift extensions, such as `Build`s, etc then simply do:

```java
OpenShiftClient osClient = new KubernetesClientBuilder().build().adapt(OpenShiftClient.class);
```

### Configuring the client

This will use settings from different sources in the following order of priority:

* System properties
* Environment variables
* Kube config file
* Service account token & mounted CA certificate

System properties are preferred over environment variables. The following system properties & environment variables can be used for configuration:

| Property / Environment Variable                                                                                 | Description                                                                                                                              | Default value                                         |
|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| `kubernetes.disable.autoConfig` / `KUBERNETES_DISABLE_AUTOCONFIG`                                               | Disable automatic configuration (KubernetesClient would not look in `~/.kube/config`, mounted ServiceAccount, environment variables or System properties for Kubernetes cluster information)                                                                                                         | `false`                                               |
| `kubernetes.master` / `KUBERNETES_MASTER`                                                                       | Kubernetes master URL                                                                                                                    | `https://kubernetes.default.svc`                      |
| `kubernetes.api.version` / `KUBERNETES_API_VERSION`                                                             | API version                                                                                                                              | `v1`                                                  |
| `openshift.url` / `OPENSHIFT_URL`                                                                               | OpenShift master URL                                                                                                                     | Kubernetes master URL value                           |
| `kubernetes.oapi.version` / `KUBERNETES_OAPI_VERSION`                                                           | OpenShift API version                                                                                                                    | `v1`                                                  |
| `kubernetes.trust.certificates` / `KUBERNETES_TRUST_CERTIFICATES`                                               | Trust all certificates                                                                                                                   | `false`                                               |
| `kubernetes.disable.hostname.verification` / `KUBERNETES_DISABLE_HOSTNAME_VERIFICATION`                         |                                                                                                                                          | `false`                                               |
| `kubernetes.certs.ca.file` / `KUBERNETES_CERTS_CA_FILE`                                                         |                                                                                                                                          |                                                       |
| `kubernetes.certs.ca.data` / `KUBERNETES_CERTS_CA_DATA`                                                         |                                                                                                                                          |                                                       |
| `kubernetes.certs.client.file` / `KUBERNETES_CERTS_CLIENT_FILE`                                                 |                                                                                                                                          |                                                       |
| `kubernetes.certs.client.data` / `KUBERNETES_CERTS_CLIENT_DATA`                                                 |                                                                                                                                          |                                                       |
| `kubernetes.certs.client.key.file` / `KUBERNETES_CERTS_CLIENT_KEY_FILE`                                         |                                                                                                                                          |                                                       |
| `kubernetes.certs.client.key.data` / `KUBERNETES_CERTS_CLIENT_KEY_DATA`                                         |                                                                                                                                          |                                                       |
| `kubernetes.certs.client.key.algo` / `KUBERNETES_CERTS_CLIENT_KEY_ALGO`                                         | Client key encryption algorithm                                                                                                          | `RSA`                                                 |
| `kubernetes.certs.client.key.passphrase` / `KUBERNETES_CERTS_CLIENT_KEY_PASSPHRASE`                             |                                                                                                                                          |                                                       |
| `kubernetes.auth.basic.username` / `KUBERNETES_AUTH_BASIC_USERNAME`                                             |                                                                                                                                          |                                                       |
| `kubernetes.auth.basic.password` / `KUBERNETES_AUTH_BASIC_PASSWORD`                                             |                                                                                                                                          |                                                       |
| `kubernetes.auth.serviceAccount.token` / `KUBERNETES_AUTH_SERVICEACCOUNT_TOKEN`                                 | Name of the service account token file                                                                                                   | `/var/run/secrets/kubernetes.io/serviceaccount/token` |
| `kubernetes.auth.tryKubeConfig` / `KUBERNETES_AUTH_TRYKUBECONFIG`                                               | Configure client using Kubernetes config                                                                                                 | `true`                                                |
| `kubeconfig` / `KUBECONFIG`                                                                                     | Name of the kubernetes config file to read                                                                                               | `~/.kube/config`                                      |
| `kubernetes.auth.tryServiceAccount` / `KUBERNETES_AUTH_TRYSERVICEACCOUNT`                                       | Configure client from Service account                                                                                                    | `true`                                                |
| `kubernetes.tryNamespacePath` / `KUBERNETES_TRYNAMESPACEPATH`                                                   | Configure client namespace from Kubernetes service account namespace path                                                                | `true`                                                |
| `kubernetes.auth.token` / `KUBERNETES_AUTH_TOKEN`                                                               |                                                                                                                                          |                                                       |
| `kubernetes.watch.reconnectInterval` / `KUBERNETES_WATCH_RECONNECTINTERVAL`                                     | Watch reconnect interval in ms                                                                                                           | `1000`                                                |
| `kubernetes.watch.reconnectLimit` / `KUBERNETES_WATCH_RECONNECTLIMIT`                                           | Number of reconnect attempts (-1 for infinite)                                                                                           | `-1`                                                  |
| `kubernetes.connection.timeout` / `KUBERNETES_CONNECTION_TIMEOUT`                                               | Connection timeout in ms (0 for no timeout)                                                                                              | `10000`                                               |
| `kubernetes.request.timeout` / `KUBERNETES_REQUEST_TIMEOUT`                                                     | Read timeout in ms                                                                                                                       | `10000`                                               |
| `kubernetes.upload.connection.timeout` / `KUBERNETES_UPLOAD_CONNECTION_TIMEOUT`                                 | Pod upload connection timeout in ms                                                                                                      | `10000`                                               |
| `kubernetes.upload.request.timeout` / `KUBERNETES_UPLOAD_REQUEST_TIMEOUT`                                       | Pod upload request timeout in ms                                                                                                         | `120000`                                              |
| `kubernetes.request.retry.backoffLimit` / `KUBERNETES_REQUEST_RETRY_BACKOFFLIMIT`                               | Number of retry attempts (-1 for infinite)                                                                                               | `10`                                                  |
| `kubernetes.request.retry.backoffInterval` / `KUBERNETES_REQUEST_RETRY_BACKOFFINTERVAL`                         | Retry initial backoff interval in ms                                                                                                     | `100`                                                 |
| `kubernetes.rolling.timeout` / `KUBERNETES_ROLLING_TIMEOUT`                                                     | Rolling timeout in ms                                                                                                                    | `900000`                                              |
| `kubernetes.logging.interval` / `KUBERNETES_LOGGING_INTERVAL`                                                   | Logging interval in ms                                                                                                                   | `20000`                                               |
| `kubernetes.scale.timeout` / `KUBERNETES_SCALE_TIMEOUT`                                                         | Scale timeout in ms                                                                                                                      | `600000`                                              |
| `kubernetes.websocket.timeout` / `KUBERNETES_WEBSOCKET_TIMEOUT`                                                 | Websocket timeout in ms                                                                                                                  | `5000`                                                |
| `kubernetes.websocket.ping.interval` / `KUBERNETES_WEBSOCKET_PING_INTERVAL`                                     | Websocket ping interval in ms                                                                                                            | `30000`                                               |
| `kubernetes.max.concurrent.requests` / `KUBERNETES_MAX_CONCURRENT_REQUESTS`                                     |                                                                                                                                          | `64`                                                  |
| `kubernetes.max.concurrent.requests.per.host` / `KUBERNETES_MAX_CONCURRENT_REQUESTS_PER_HOST`                   |                                                                                                                                          | `5`                                                   |
| `kubernetes.impersonate.username` / `KUBERNETES_IMPERSONATE_USERNAME`                                           | `Impersonate-User` HTTP header value                                                                                                     |                                                       |
| `kubernetes.impersonate.group` / `KUBERNETES_IMPERSONATE_GROUP`                                                 | `Impersonate-Group` HTTP header value                                                                                                    |                                                       |
| `kubernetes.tls.versions` / `KUBERNETES_TLS_VERSIONS`                                                           | TLS versions separated by `,`                                                                                                            | `TLSv1.2,TLSv1.3`                                     |
| `kubernetes.truststore.file` / `KUBERNETES_TRUSTSTORE_FILE`                                                     |                                                                                                                                          |                                                       |
| `kubernetes.truststore.passphrase` / `KUBERNETES_TRUSTSTORE_PASSPHRASE`                                         |                                                                                                                                          |                                                       |
| `kubernetes.keystore.file` / `KUBERNETES_KEYSTORE_FILE`                                                         |                                                                                                                                          |                                                       |
| `kubernetes.keystore.passphrase` / `KUBERNETES_KEYSTORE_PASSPHRASE`                                             |                                                                                                                                          |                                                       |
| `kubernetes.backwardsCompatibilityInterceptor.disable` / `KUBERNETES_BACKWARDSCOMPATIBILITYINTERCEPTOR_DISABLE` | Disable the `BackwardsCompatibilityInterceptor`                                                                                          | `true`                                                |
| `no.proxy` / `NO_PROXY`                                                                                         | comma-separated list of domain extensions [proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html) should not be used for |                                                       |
| `http.proxy` / `HTTP_PROXY`                                                                                     | URL to the [proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html) for HTTP requests (See [Proxy precedence](./doc/FAQ.md#how-does-kubernetesclient-loads-proxy-url-from-various-sources))                                    |                                                       |
| `https.proxy` / `HTTPS_PROXY`                                                                                   | URL to the [proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html) for HTTPS requests (See [Proxy precedence](./doc/FAQ.md#how-does-kubernetesclient-loads-proxy-url-from-various-sources))                                   |                                                       |

Alternatively you can use the `ConfigBuilder` to create a config object for the Kubernetes client:

```java
Config config = new ConfigBuilder().withMasterUrl("https://mymaster.com").build();
KubernetesClient client = new KubernetesClientBuilder().withConfig(config).build();
```

###
Using the DSL is the same for all resources.

List resources:

```java
NamespaceList myNs = client.namespaces().list();

ServiceList myServices = client.services().list();

ServiceList myNsServices = client.services().inNamespace("default").list();
```

Get a resource:

```java
Namespace myns = client.namespaces().withName("myns").get();

Service myservice = client.services().inNamespace("default").withName("myservice").get();
```

Delete:

```java
Namespace myns = client.namespaces().withName("myns").delete();

Service myservice = client.services().inNamespace("default").withName("myservice").delete();
```

Editing resources uses the inline builders from the Kubernetes Model:

```java
Namespace myns = client.namespaces().withName("myns").edit(n -> new NamespaceBuilder(n)
                   .editMetadata()
                     .addToLabels("a", "label")
                   .endMetadata()
                   .build());

Service myservice = client.services().inNamespace("default").withName("myservice").edit(s -> new ServiceBuilder(s)
                     .editMetadata()
                       .addToLabels("another", "label")
                     .endMetadata()
                     .build());
```

In the same spirit you can inline builders to create:

```java
Namespace myns = client.namespaces().create(new NamespaceBuilder()
                   .withNewMetadata()
                     .withName("myns")
                     .addToLabels("a", "label")
                   .endMetadata()
                   .build());

Service myservice = client.services().inNamespace("default").create(new ServiceBuilder()
                     .withNewMetadata()
                       .withName("myservice")
                       .addToLabels("another", "label")
                     .endMetadata()
                     .build());
```

You can also set the apiVersion of the resource like in the case of SecurityContextConstraints :

```java
SecurityContextConstraints scc = new SecurityContextConstraintsBuilder()
		.withApiVersion("v1")
		.withNewMetadata().withName("scc").endMetadata()
		.withAllowPrivilegedContainer(true)
		.withNewRunAsUser()
		.withType("RunAsAny")
		.endRunAsUser()
		.build();
```

### Following events

Use `io.fabric8.kubernetes.api.model.Event` as T for Watcher:

```java
client.events().inAnyNamespace().watch(new Watcher<>() {

  @Override
  public void eventReceived(Action action, Event resource) {
    System.out.println("event " + action.name() + " " + resource.toString());
  }

  @Override
  public void onClose(WatcherException cause) {
    System.out.println("Watcher close due to " + cause);
  }

});
```

### Working with extensions

The kubernetes API defines a bunch of extensions like `daemonSets`, `jobs`, `ingresses` and so forth which are all usable in the `extensions()` DSL:

e.g. to list the jobs...

```
jobs = client.batch().jobs().list();
```

### Loading resources from external sources

There are cases where you want to read a resource from an external source, rather than defining it using the clients DSL.
For those cases the client allows you to load the resource from:

- A file *(Supports both java.io.File and java.lang.String)*
- A url
- An input stream

Once the resource is loaded, you can treat it as you would, had you created it yourself.

For example lets read a pod, from a yml file and work with it:

    Pod refreshed = client.load('/path/to/a/pod.yml').fromServer().get();
    client.load('/workspace/pod.yml').delete();
    LogWatch handle = client.load('/workspace/pod.yml').watchLog(System.out);

### Passing a reference of a resource to the client

In the same spirit you can use an object created externally (either a reference or using its string representation).

For example:

    Pod pod = someThirdPartyCodeThatCreatesAPod();
    client.resource(pod).delete();

### Adapting the client

The client supports plug-able adapters. An example adapter is the [OpenShift Adapter](openshift-client/src/main/java/io/fabric8/openshift/client/impl/OpenShiftExtensionAdapter.java)
which allows adapting an existing [KubernetesClient](kubernetes-client-api/src/main/java/io/fabric8/kubernetes/client/KubernetesClient.java) instance to an [OpenShiftClient](openshift-client-api/src/main/java/io/fabric8/openshift/client/OpenShiftClient.java) one.

 For example:

```java
KubernetesClient client = new KubernetesClientBuilder().build();

OpenShiftClient oClient = client.adapt(OpenShiftClient.class);
```

The client also support the isAdaptable() method which checks if the adaptation is possible and returns true if it does.

```java
KubernetesClient client = new KubernetesClientBuilder().build();
if (client.isAdaptable(OpenShiftClient.class)) {
    OpenShiftClient oClient = client.adapt(OpenShiftClient.class);
} else {
    throw new Exception("Adapting to OpenShiftClient not support. Check if adapter is present, and that env provides /oapi root path.");
}
```

#### Adapting and close
Note that when using adapt() both the adaptee and the target will share the same resources (underlying http client, thread pools etc).
This means that close() is not required to be used on every single instance created via adapt.
Calling close() on any of the adapt() managed instances or the original instance, will properly clean up all the resources and thus none of the instances will be usable any longer.


## Mocking Kubernetes

Along with the client this project also provides a Kubernetes Mock Server that you can use for testing purposes.

The Mock Web Server has two modes of operation:

- Expectations mode
- CRUD mode

### Expectations mode

In this mode, you can set up expectations for the server to respond to HTTP and websocket requests.

This mode has been extensively used for testing the client itself.
Make sure you check [kubernetes-test](kubernetes-tests/src/test/java/io/fabric8/kubernetes/client/mock).

To add a Kubernetes server to your test:
```java
@EnableKubernetesMockClient
class MyTestSuite {
  KubernetesMockServer server;
}
```

Then you can use the server to define the expectations and the client to perform the regular kubernetes operations:
```java
class MyTestSuite {
  KubernetesMockServer server;
  KubernetesClient client;

  @Test
  void myTest() {
    server.expect().get()
      .withPath("/api/v1/namespaces/my-namespace/pods/my-pod")
      .andReturn(200, new PodBuilder().build())
      .always();
    Pod pod = client.pods().inNamespace("my-namespace").withName("my-pod").get();
  }
}
```

### CRUD mode

Defining every single request and response can become tiresome.
Given that in most cases the Mock Server is mostly used to perform simple CRUD based operations, a CRUD mode is also available.

When using the CRUD mode, the mock web server will store, read, update and delete kubernetes resources using an in memory map and will appear as a real API server.

To add a Kubernetes Server in crud mode to your test:
```java
@EnableKubernetesMockClient(crud = true)
class MyTestSuite {
  KubernetesClient client;
}
```

Then you can use the client to perform the regular kubernetes operations:
```java
class MyTestSuite {
  KubernetesClient client;

  @Test
  public void myCrudTest() {
    //CREATE
    client.pods().inNamespace("ns1").create(new PodBuilder().withNewMetadata().withName("pod1").endMetadata().build());

    //READ
    podList = client.pods().inNamespace("ns1").list();
    assertNotNull(podList);
    assertEquals(1, podList.getItems().size());
  }
}
```

## Testing Against real Kubernetes API Server with Kube API Test

In order to test against real Kubernetes API the project provides a lightweight approach, thus starting up Kubernetes API Server and etcd binaries.

```java
@EnableKubeAPIServer
class KubeAPITestSample {

  static KubernetesClient client;
  
  @Test
  void testWithClient() {
    // test using the client against real K8S API Server   
  }
}
```

For details see docs for [Kube API Test](doc/kube-api-test.md).

## Compatibility

### Kubernetes

Starting from v5.5, the Kubernetes Client should be compatible with **any** supported Kubernetes cluster version.
We provide DSL methods (for example `client.pods()`, `client.namespaces()`, and so on) for the most commonly used Kubernetes resources. If the resource you're looking for is not available through the DSL, you can always use the generic `client.resource()` method to interact with it. You can also open a [new issue](https://github.com/fabric8io/kubernetes-client/issues/new/choose) to request the addition of a new resource to the DSL.

We provide Kubernetes Java model types (for example `Pod`) and their corresponding builders (for example `PodBuilder`) for every vanilla Kubernetes resource (and some extensions). If you don't find a specific resource, and you think that it should be part of the Kubernetes Client, please open a [new issue](https://github.com/fabric8io/kubernetes-client/issues/new/choose).

### OpenShift

Starting from v5.5, the OpenShift Client should be compatible with **any** OpenShift cluster version currently supported by Red Hat.
The Fabric8 Kubernetes Client is one of the few Kubernetes Java clients that provides full support for any supported OpenShift cluster version. If you find any incompatibility or something missing, please open a [new issue](https://github.com/fabric8io/kubernetes-client/issues/new/choose).


## Major Changes in Kubernetes Client 4.0.0
All the resource objects used here will be according to OpenShift 3.9.0  and Kubernetes 1.9.0. All the resource objects will give all the fields according to OpenShift 3.9.0 and Kubernetes 1.9.0

* SecurityContextConstraints has been moved to OpenShift client from Kubernetes Client
* Job dsl is in both `batch` and `extensions`(Extensions is deprecated)
* DaemonSet dsl is in both `apps` and `extensions`(Extensions is deprecated)
* Deployment dsl is in both `apps` and `extensions`(Extensions is deprecated)
* ReplicaSet dsl is in both `apps` and `extensions`(Extensions is deprecated)
* NetworkPolicy dsl is in both `network` and `extensions`(Extensions is deprecated)
* Storage Class moved from `client base DSL` to `storage` DSL
* PodSecurityPolicies moved from `client base DSL` and `extensions` to only `extensions`
* ThirdPartyResource has been removed.

## Who uses Kubernetes & OpenShift Java client?

  Extensions:
  - [Knative](https://github.com/fabric8io/kubernetes-client/tree/master/extensions/knative)
  - [Tekton](https://github.com/fabric8io/kubernetes-client/tree/master/extensions/tekton)
  - [Volcano](https://github.com/fabric8io/kubernetes-client/tree/master/extensions/volcano)
  - [Istio](https://github.com/fabric8io/kubernetes-client/tree/master/extensions/istio)
  - [Open Cluster Management](https://github.com/fabric8io/kubernetes-client/tree/master/extensions/open-cluster-management)
  - [Camel-k](https://camel.apache.org/camel-k/next/apis/java.html) - [Maven Central](https://search.maven.org/artifact/org.apache.camel.k/camel-k-crds)

  Frameworks/Libraries/Tools:
  - [Arquillian Cube](http://arquillian.org/arquillian-cube/)
  - [Apache Camel](https://github.com/apache/camel/blob/master/README.md)
  - [Apache Flink](https://github.com/apache/flink/tree/master/flink-kubernetes)
  - [Apache Spark](https://github.com/apache/spark/tree/master/resource-managers/kubernetes)
  - [Jaeger Kubernetes](https://github.com/jaegertracing/jaeger-kubernetes)
  - [Loom](https://github.com/datawire/loom)
  - [Microsoft Azure Libraries for Java](https://github.com/Azure/azure-libraries-for-java)
  - [Spinnaker Halyard](https://github.com/spinnaker/halyard)
  - [Spring Cloud Connectors for Kubernetes](https://github.com/spring-cloud/spring-cloud-kubernetes-connector)
  - [Spring Cloud Kubernetes](https://github.com/fabric8io/spring-cloud-kubernetes)

  CI Plugins:
  - [Deployment Pipeline Plugin (Jenkins)](https://github.com/pearsontechnology/deployment-pipeline-jenkins-plugin)
  - [Kubernetes Elastic Agent (GoCD)](https://github.com/gocd/kubernetes-elastic-agents)
  - [Kubernetes Plugin (Jenkins)](https://github.com/jenkinsci/kubernetes-plugin)
  - [Kubernetes Pipeline Plugin (Jenkins)](https://github.com/jenkinsci/kubernetes-pipeline-plugin)
  - [OpenShift Sync Plugin (Jenkins)](https://github.com/openshift/jenkins-sync-plugin)
  - [Kubernetes Plugin (Teamcity from Jetbrains)](https://github.com/JetBrains/teamcity-kubernetes-plugin)
  - [Kubernetes Agents for Bamboo (WindTunnel Technologies)](https://marketplace.atlassian.com/apps/1222674/kubernetes-agents-for-bamboo)

  Build Tools:
  - [Fabric8 Maven Plugin](https://github.com/fabric8io/fabric8-maven-plugin)
  - [Eclipse JKube](https://github.com/eclipse/jkube)
  - [Gradle Kubernetes Plugin](https://github.com/bmuschko/gradle-kubernetes-plugin)

  Platforms:
  - [Apache Openwhisk](https://github.com/apache/incubator-openwhisk)
  - [Eclipse che](https://www.eclipse.org/che/)
  - [Openshift.io (Launcher service)](https://github.com/fabric8-launcher)
  - [Spotify Styx](https://github.com/spotify/styx)
  - [Strimzi](https://github.com/strimzi/)
  - [Syndesis](https://syndesis.io/)
  - [StackGres](https://stackgres.io/)
  - [Boomerang Flow](https://github.com/boomerang-io)
  - [Apache Kyuubi](https://github.com/apache/kyuubi)

  Proprietary Platforms:
  - [vCommander](https://www.embotics.com/hybrid-cloud-management-platform)

As our community grows, we would like to track keep track of our users. Please send a PR with your organization/community name.

## Tests we run for every new Pull Request
There are the links of the Github Actions and Jenkins for the tests which run for every new Pull Request. You can view all the recent builds also.

* [Regression Tests](https://github.com/fabric8io/kubernetes-client/actions)
* [Unit Tests](https://ci.fabric8.io/job/kubernetes-client-pullreq/)

To get the updates about the releases, you can join https://groups.google.com/forum/embed/?place=forum/fabric8-devclients

## Kubectl Java Equivalents
This table provides `kubectl` to Kubernetes Java Client mappings. Most of the mappings are quite straightforward and are one liner
operations. However, some might require slightly more code to achieve same result:

| kubectl                                                                          | Fabric8 Kubernetes Client                                                                                                                                                                         |
|----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kubectl config view`                                                            | [ConfigViewEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigViewEquivalent.java)                                                     |
| `kubectl config get-contexts`                                                    | [ConfigGetContextsEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigGetContextsEquivalent.java)                                       |
| `kubectl config current-context`                                                 | [ConfigGetCurrentContextEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigGetCurrentContextEquivalent.java)                           |
| `kubectl config use-context minikube`                                            | [ConfigUseContext.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigUseContext.java)                                                             |
| `kubectl config view -o jsonpath='{.users[*].name}'`                             | [ConfigGetCurrentContextEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigGetCurrentContextEquivalent.java)                           |
| `kubectl get pods --all-namespaces`                                              | [PodListGlobalEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodListGlobalEquivalent.java)                                               |
| `kubectl get pods`                                                               | [PodListEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodListEquivalent.java)                                                           |
| `kubectl get pods -w`                                                            | [PodWatchEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodWatchEquivalent.java)                                                         |
| `kubectl get pods --sort-by='.metadata.creationTimestamp'`                       | [PodListGlobalEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodListGlobalEquivalent.java)                                               |
| `kubectl run`                                                                    | [PodRunEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodRunEquivalent.java)                                                             |
| `kubectl create -f test-pod.yaml`                                                | [PodCreateYamlEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodCreateYamlEquivalent.java)                                               |
| `kubectl exec my-pod -- ls /`                                                    | [PodExecEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodExecEquivalent.java)                                                           |
| `kubectl attach my-pod`                                                          | [PodAttachEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodAttachEquivalent.java)                                                       |
| `kubectl delete pod my-pod`                                                      | [PodDelete.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodDelete.java)                                                                           |
| `kubectl delete -f test-pod.yaml`                                                | [PodDeleteViaYaml.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodDeleteViaYaml.java)                                                             |
| `kubectl cp /foo_dir my-pod:/bar_dir`                                            | [UploadDirectoryToPod.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/UploadDirectoryToPod.java)                                                     |
| `kubectl cp my-pod:/tmp/foo /tmp/bar`                                            | [DownloadFileFromPod.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/DownloadFileFromPod.java)                                                       |
| `kubectl cp my-pod:/tmp/foo -c c1 /tmp/bar`                                      | [DownloadFileFromMultiContainerPod.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/DownloadFileFromMultiContainerPod.java)                           |
| `kubectl cp /foo_dir my-pod:/tmp/bar_dir`                                        | [UploadFileToPod.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/UploadFileToPod.java)                                                               |
| `kubectl logs pod/my-pod`                                                        | [PodLogsEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodLogsEquivalent.java)                                                           |
| `kubectl logs pod/my-pod -f`                                                     | [PodLogsFollowEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodLogsFollowEquivalent.java)                                               |
| `kubectl logs pod/my-pod -c c1`                                                  | [PodLogsMultiContainerEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodLogsMultiContainerEquivalent.java)                               |
| `kubectl port-forward my-pod 8080:80`                                            | [PortForwardEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PortForwardEquivalent.java)                                                   |
| `kubectl get pods --selector=version=v1 -o jsonpath='{.items[*].metadata.name}'` | [PodListFilterByLabel.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodListFilterByLabel.java)                                                     |
| `kubectl get pods --field-selector=status.phase=Running`                         | [PodListFilterFieldSelector.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodListFilterFieldSelector.java)                                         |
| `kubectl get pods --show-labels`                                                 | [PodShowLabels.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodShowLabels.java)                                                                   |
| `kubectl label pods my-pod new-label=awesome`                                    | [PodAddLabel.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodAddLabel.java)                                                                       |
| `kubectl annotate pods my-pod icon-url=http://goo.gl/XXBTWq`                     | [PodAddAnnotation.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/PodAddAnnotation.java)                                                             |
| `kubectl get configmap cm1 -o jsonpath='{.data.database}'`                       | [ConfigMapJsonPathEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ConfigMapJsonPathEquivalent.java)                                       |
| `kubectl create -f test-svc.yaml`                                                | [LoadAndCreateService.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/LoadAndCreateService.java)                                                     |
| `kubectl create -f test-deploy.yaml`                                             | [LoadAndCreateDeployment.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/LoadAndCreateDeployment.java)                                               |
| `kubectl set image deploy/d1 nginx=nginx:v2`                                     | [RolloutSetImageEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/RolloutSetImageEquivalent.java)                                           |
| `kubectl scale --replicas=4 deploy/nginx-deployment`                             | [ScaleEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ScaleEquivalent.java)                                                               |
| `kubectl scale statefulset --selector=app=my-database --replicas=4`              | [ScaleWithLabelsEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/ScaleWithLabelsEquivalent.java)                                           |
| `kubectl rollout restart deploy/d1`                                              | [RolloutRestartEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/RolloutRestartEquivalent.java)                                             |
| `kubectl rollout pause deploy/d1`                                                | [RolloutPauseEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/RolloutPauseEquivalent.java)                                                 |
| `kubectl rollout resume deploy/d1`                                               | [RolloutResumeEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/RolloutResumeEquivalent.java)                                               |
| `kubectl rollout undo deploy/d1`                                                 | [RolloutUndoEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/RolloutUndoEquivalent.java)                                                   |
| `kubectl create -f test-crd.yaml`                                                | [LoadAndCreateCustomResourceDefinition.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/LoadAndCreateCustomResourceDefinition.java)                   |
| `kubectl create -f customresource.yaml`                                          | [CustomResourceCreateDemo.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CustomResourceCreateDemo.java)                                             |
| `kubectl create -f customresource.yaml`                                          | [CustomResourceCreateDemoTypeless.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CustomResourceCreateDemoTypeless.java)                             |
| `kubectl get ns`                                                                 | [NamespaceListEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/NamespaceListEquivalent.java)                                               |
| `kubectl create namespace test`                                                                 | [NamespaceCreateEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/NamespaceCreateEquivalent.java)                                               |
| `kubectl apply -f test-resource-list.yml`                                        | [CreateOrReplaceResourceList.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CreateOrReplaceResourceList.java)                                       |
| `kubectl get events`                                                             | [EventsGetEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/EventsGetEquivalent.java)                                                       |
| `kubectl events --for jobs/jobName`                                              | [EventsGetForJobEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/EventsGetForJobEquivalent.java)                                        |
| `kubectl top nodes`                                                              | [TopEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/TopEquivalent.java)                                                                   |
| `kubectl auth can-i create deployment.apps`                                      | [CanIEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CanIEquivalent.java)                                                                 |
| `kubectl create -f test-csr-v1.yml`                                              | [CertificateSigningRequestCreateYamlEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CertificateSigningRequestCreateYamlEquivalent.java)   |
| `kubectl certificate approve my-cert`                                            | [CertificateSigningRequestApproveYamlEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CertificateSigningRequestApproveYamlEquivalent.java) |
| `kubectl certificate deny my-cert`                                               | [CertificateSigningRequestDenyYamlEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CertificateSigningRequestDenyYamlEquivalent.java)       |
| `kubectl create -f quota.yaml --namespace=default`                               | [CreateResourceQuotaInNamespaceYamlEquivalent.java](./kubernetes-examples/src/main/java/io/fabric8/kubernetes/examples/kubectl/equivalents/CreateResourceQuotaInNamespaceYamlEquivalent.java)     |
