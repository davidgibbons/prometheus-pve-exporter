# Prometheus PVE Exporter Helm Chart

## Description

The **Prometheus PVE Exporter** Helm chart provides a straightforward way to deploy the `prometheus-pve-exporter` on Kubernetes. This exporter enables Prometheus to scrape metrics from Proxmox VE (Virtual Environment) servers, enhancing your monitoring setup with Proxmox metrics.

## Usage

To use this Helm chart, you first need to have Helm installed on your Kubernetes cluster. Once you have Helm set up, you can deploy the chart using the following steps:

1. **Clone the Helm repository:**
   ```bash
   git clone https://github.com/zgs225/prometheus-pve-exporter
   ```

2. **Install the chart:**
   ```bash
   cd prometheus-pve-exporter
   helm install <my-release> .
   ```

   Replace `my-release` with a name for your Helm release.

3. **Verify the installation:**
   ```bash
   helm list
   ```

4. **Get the status of your deployment:**
   ```bash
   kubectl get all -l release=my-release
   ```

## Configuration

The chart's configuration is managed through the `values.yaml` file. Below are the key configuration options you can set:

### Proxmox Authentication Config

Specify the authentication method for accessing Proxmox VE servers. You can choose between token authentication and user authentication.

#### Token Authentication (Preferred)

```yaml
authentication:
  default:
    user: <your-username>
    token_name: <your-token-name>
    token_value: <your-token-value>
    verify_ssl: false
```

- `user`: Proxmox VE user for authentication.
- `token_name`: Name of the token.
- `token_value`: Value of the token.
- `verify_ssl`: Set to `true` to enable SSL verification. Default is `false`.

#### User Authentication (Alternative)

```yaml
authentication:
  default:
    user: <your-username>
    password: <your-password>
    verify_ssl: false
```

- `user`: Proxmox VE user for authentication.
- `password`: Password for the user.
- `verify_ssl`: Set to `true` to enable SSL verification. Default is `false`.

### Proxmox VE Servers' Hostnames

Define the list of Proxmox VE servers from which to scrape metrics.

```yaml
scrapeTargets:
  - <hostname1>
  - <hostname2>
```

Replace `<hostname1>` and `<hostname2>` with the hostnames or IP addresses of your Proxmox VE servers.

### ScrapeConfig Namespace

Specify the namespace where the ScrapeConfig CRD will be created. By default, this is set to the namespace of the Helm release.

```yaml
scrapeConfigNamespace: <namespace>
```

Replace `<namespace>` with the desired namespace for the ScrapeConfig CRD. If left blank, the chart will use the release namespace.

## Example Configuration

Here is an example `values.yaml` configuration:

```yaml
authentication:
  default:
    user: admin
    token_name: my-token
    token_value: my-token-value
    verify_ssl: true

scrapeTargets:
  - 192.168.1.10
  - 192.168.1.11

scrapeConfigNamespace: monitoring
```

This configuration sets up token-based authentication, targets two Proxmox VE servers, and places the ScrapeConfig CRD in the `monitoring` namespace.

## Notes

- Ensure that Proxmox VE servers are accessible from your Kubernetes cluster.
- Review the Prometheus documentation for additional configuration options and best practices for setting up scrape targets.

For more detailed information, consult the [Prometheus PVE Exporter documentation](https://github.com/<your-repo>/prometheus-pve-exporter).
