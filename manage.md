---

copyright:
  years: 2019
lastupdated: "2019-08-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Managing the cluster
{: #manage}

## Common tasks
{: #common-management-tasks}

You can use Kubernetes commands or OpenShift commands to perform tasks that you cannot perform from the {{site.data.keyword.icp4dfull}} web client.

### To identify which nodes the product is deployed to
{: #identify-nodes}

```bash
kubectl get pods -o wide
```
{: pre}

With OpenShift:

```bash
oc get pods -o wide
```
{: pre}

### To find out how many replicas are in use
{: #get-replicas-in-use}

```bash
kubectl get deploy -n {namespace-name}
```
{: pre}

```bash
kubectl get statefulset -n {namespace-name}
```
{: pre}

With OpenShift:

```bash
oc get deploy -n {namespace-name}
```
{: pre}

```bash
oc get statefulset -n {namespace-name}
```
{: pre}

The response shows you name and number of replicas.

## Scaling
{: #scaling}

The following sections describe the recommended minimum production requirements to install Watson Natural Language Understanding, as well as instructions for scaling Deployments and configuring StatefulSets.

You can install with custom configurations by editing the `dev-value-overrides.yaml` or `prod-value-verrides.yaml` files.

### Deployments
{: #deployments}

| Component Name | Deployment Name | Pod Name | Default Number of Replicas | Notes |  
| :------------- | :-------------- | :------- | :-------------------- | :---- |
| Sentiment | {release-name}-ibm-sentiment-sentiment-analysis-en | {release-name}-ibm-sentiment-sentiment-analysis-en-{xxxxxxxxxx-xxxxx} | 2 | |
| Model Management API | {release-name}-ibm-watson-mma-prod-model-management-api | {release-name}-ibm-watson-mma-prod-model-management-api-{xxxxxxxxxx-xxxxx} | 2 | |
| Text Processing | {release-name}-ibm-watson-nlp-api | {release-name}-ibm-watson-nlp-api-{xxxxxxxxxx-xxxxx} | 2 | |
| Keywords Feature | {release-name}-ibm-watson-nlu-prod-keywords | {release-name}-ibm-watson-nlu-prod-keywords- {xxxxxxxxxx-xxxxx} | 2 | |
| NLU Server | {release-name}-ibm-watson-nlu-prod-nluserver | {release-name}-ibm-watson-nlu-prod-nluserver-{xxxxxxxxxx-xxxxx} | 2 | |
| Orchestrator | {release-name}-ibm-watson-nlu-prod-orchestrator | {release-name}-ibm-watson-nlu-prod-orchestrator-{xxxxxxxxxx-xxxxx} | 2 | |
| Models Server | {release-name}-ibm-watson-nms-prod-models-server | {release-name}-ibm-watson-nms-prod-models-server-{xxxxxxxxxx-xxxxx} | 1 | |
| PostgreSQL | {release-name}-postgres-proxy | {release-name}-postgres-proxy-{xxxxxxxxxx-xxxxx} | 2 | Replicas must be >= 2 |
| PostgreSQL | {release-name}-postgres-sentinel | {release-name}-postgres-sentinel-{xxxxxxxxxx-xxxxx} | 3 |  Replicas must be >= 3 |
| Relationship Extraction | {release-name}-sire-runtime-model-mesh | {release-name}-sire-runtime-model-mesh-{xxxxxxxxxx-xxxxx} | 2 | |
| Relationship Extraction Dashboard | {release-name}-sire-runtime-model-mesh-dashboard | {release-name}-sire-runtime-model-mesh-dashboard-{xxxxxxxxxx-xxxxx} | 0 | |

- {release name} is the Helm release name of your installation.

To scale the number of replicas for Deployments, use the `kubectl scale` command, or the `oc scale` command if you are using OpenShift.
```bash
kubectl scale deployment/{deployment_name} --replicas={count}
```
{: pre}

```bash
oc scale deployment/{deployment_name} --replicas={count}
```
{: pre}

- `{deployment_name}` is the name of the Deployment you want to scale, which should be one of the Deployment names listed above.
- `{count}` is the expected number of replicas to be scaled.

For example, if you want to scale up the Deployment of the NLU server, associated with the release `my-release`, from 1 to 2 replicas. the command will be:

```bash
kubectl scale deployment/my-release--ibm-watson-nlu-prod-nluserver --replicas=2
```
{: pre}

With OpenShift:

```bash
oc scale deployment/my-release--ibm-watson-nlu-prod-nluserver --replicas=2
```
{: pre}

### Statefulsets
{: #statefulsets}

| Component Name | Statefulset Name | Pod Name | Default Number of Replicas | Notes |  
| :------------- | :--------------- | :------- | :-------------------- | :---- |
| ETCD | {release-name}-ibm-etcd | {release-name}-ibm-etcd-{pod-number} | 5 | Scale replicas in odd numbers; must be >= 5 |
| MinIO | {release-name}-ibm-minio | {release-name}-ibm-minio-{pod-number} | 4 | Scale replicas in even numbers; must be >= 4 |
| PostgreSQL | {release-name}-postgres-keeper | {release-name}-postgres-keeper-{pod-number} | 3 | Replicas must be >= 3 |

- {release name} is the Helm release name of your installation.
- {pod-number} is a number between 0 and one less than the replica count

Datastore StatefulSets cannot be scaled after an installation. To install with replicas other than the default values listed above, edit the `/ibm/InstallPackage/modules/nlu/dev-value-overrides.yaml` or `/ibm/InstallPackage/modules/nlu/prod-value-overrides.yaml` file before the installation. You will change the field "replica" or "replicaCount" for the corresponding component in the appropriate (dev or prod) yaml file. 

For example, to change the number of replicas for MinIO from 4 to 6, as shown in the following lines:

```bash
minio:
  replicas: 6
```
{: pre}

Then, run the `.deploy.sh` installation command, pointing at the file you just changed.

```bash
./deploy.sh -O /ibm/InstallPackage/modules/nlu/{dev-or-prod}-value-overrides.yaml -e {release_name}`
```
{: pre}

The {{site.data.keyword.nlushort}} service has only been tested with the default number of replicas for each StatefulSet listed.
{: note}

## Viewing logs
{: #viewing-logs}

{{site.data.keyword.icp4dfull_notm}} automatically logs information from each service. For more information, see [Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}

Also see [Integrating with Grafana or Kibana dashboards](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/admindash-integrate.html#admindash-integrate){: external}.

## Managing user access
{: #managing-user-access}

After you provision an instance, you can share the URL for the service with other users. However, those users can log in to the service only if you give them access.

If you plan to use SAML for single sign-on (SSO), complete [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) before you add users. If you add users before you configure SSO, you need to re-add the users with their SAML IDs to enable them to use SSO.

1.  From the web client menu, click **Administer > Manage user**.

1.  Click **Add user**, then specify the user's full name, user name, and email address. Set the user's permissions, and then click **Add**.

1.  From the web client menu, select **My Instances**.

1.  Find your {{site.data.keyword.nlushort}} instance, click the more (**...**) menu, and then choose **Manage Access**.

1.  Click **Add user**.

1.  Click the user name field to see a list of the people you can add.

    The users you added in the previous steps are listed. Select a name, choose **User** or **Admin** as their access role, and then click **Add**.

    If you are not connected to an existing user registry and have not enabled single sign-on, then temporary passwords are created for the users you add. The temporary passwords are sent to users by way of the email addresses you specified.

