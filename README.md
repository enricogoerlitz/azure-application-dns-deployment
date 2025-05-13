# Azure Application DNS Deployment

## Motivation

This project explores how to configure custom DNS settings for applications deployed across different Azure services. It showcases three deployment models, each bound to a custom domain, allowing developers and architects to understand the process of domain binding, DNS record setup, and service-specific configurations:

- [App Service Deployment](https://app-service-deployment.enricogoerlitz.com/)
- [Container Apps Deployment](https://container-apps-deployment.enricogoerlitz.com/)
- [Front Door Deployment](https://front-door-deployment.enricogoerlitz.com/)

All deployments demonstrate how to use custom subdomains managed via AWS Route 53 for DNS hosting, emphasizing interoperability and cross-cloud DNS management.

---

## DNS Setup for App Service Deployment

### Architecture

![App Service Architecture](/app-service-deployment/architecture/app-service-deployment.drawio.png)

### Configuration Steps

#### 1. Deploy Infrastructure

```bash
$ terraform apply
```

#### 2. Configure Custom Domain

- Navigate to the App Service → `Custom domains`
- Click on "Add custom domain"

![Add custom domain](/_resources/setup-app-service-deployment/02-create-custom-domain.png)

- Add a CNAME or A-Record and the required TXT record to your domain provider (Route 53 in this case):

![DNS Settings](/_resources/setup-app-service-deployment/01-dns-settings-route53.png)

- Validate the domain ownership and confirm the binding:

![App Service Deployment verification](/_resources/setup-app-service-deployment/03-custom-domain-verify.png)

> Note: DNS propagation can take up to 5 minutes.

#### 3. Verify Deployment

Visit: [https://app-service-deployment.enricogoerlitz.com/](https://app-service-deployment.enricogoerlitz.com/)

![App Service Deployment URL](/_resources/setup-app-service-deployment/04-confirm-url.png)

---

## DNS Setup for Container Apps Deployment

### Architecture

![Container Apps Architecture](/container-apps-deployment/architecture/container-apps-deployment.drawio.png)

### Configuration Steps

#### 1. Deploy Infrastructure

```bash
$ terraform apply
```

#### 2. Configure Custom Domain

- Navigate to Container Apps → `Custom domains`
- Click on "Add custom domain"

![Add custom domain](/_resources/setup-container-apps-deployment/02-create-custom-domain.png)

- Add a CNAME or A-Record and the required TXT record to your domain provider:

![DNS Settings](/_resources/setup-app-service-deployment/01-dns-settings-route53.png)

- Validate the domain ownership and confirm the binding:

![Container Apps Deployment verification](/_resources/setup-container-apps-deployment/03-custom-domain-verify.png)

> Note: DNS propagation can take up to 5 minutes.

#### 3. Verify Deployment

Visit: [https://container-apps-deployment.enricogoerlitz.com/](https://container-apps-deployment.enricogoerlitz.com/)

![Container Apps Deployment URL](/_resources/setup-container-apps-deployment/04-confirm-url.png)

---

## DNS Setup for Front Door Deployment

### Architecture

![Front Door Deployment Architecture](/storage-account-front-door-deployment/architecture/front-door-deployment.drawio.png)

### Configuration Steps

#### 1. Deploy Infrastructure

```bash
$ terraform apply
```

#### 2. Configure Custom Domain

- Create a new domain in the Front Door Manager:

![Add a domain](/_resources/setup-storage-account-front-door-deployment/01-create-domain.png)

- Click on the "Pending" status and add the TXT record provided by Azure to your DNS provider:

![Pending state](/_resources/setup-storage-account-front-door-deployment/02-domain-pending-dns-txt-record.png)

- Associate the domain with the appropriate Front Door endpoint.

- In your DNS provider, create a CNAME record:
  
  ```
  CNAME: front-door-deployment.enricogoerlitz.com → <azure_fd_endpoint>.azurefd.net
  ```

- Confirm domain association in the Front Door manager:

![Verify Front Door manager endpoint config](/_resources/setup-storage-account-front-door-deployment/03-confirm-domain-association.png)

> Wait a few minutes for the domain binding to complete.

#### 3. Verify Deployment

Visit: [https://front-door-deployment.enricogoerlitz.com/](https://front-door-deployment.enricogoerlitz.com/)

![Front Door Deployment URL](/_resources/setup-storage-account-front-door-deployment/04-confirm-url.png)
