# DNS Updater

DNS Updater is a Python-based tool that automatically updates Cloudflare DNS records with your public IP address. If your server's IP address changes frequently or you have dynamic ip, this tool ensures that your domains and subdomains always point to the correct server. It can handle multiple domains and subdomains from multiple zones, with proxying enabled or disabled. The tool runs checks and updates every 5 minutes and includes redundancy for IP checking services.

## Features

- Update multiple domains/subdomains from different zones
- Enable or disable proxying for each domain
- Redundancy for IP checking services
- Automatically runs checks and updates every 5 minutes
- Docker support for easy deployment

## Prerequisites

- Python 3.11
- Docker (optional)

## Installation

Clone the repository:

```
git clone https://github.com/alexplesoiu/dns-updater.git
cd dns-updater
```


Install the required Python packages:
```
pip install -r requirements.txt
```

## Configuration

Edit the .env file with your actual data to configure the script, or if you don't want to use environment variables change the `update_dns.py` script, set `USE_ENV` to False and replace the placeholders for `API_KEY`, `EMAIL`, and the `DOMAINS_TO_UPDATE` list as shown below.

Example configuration:
```
API_KEY = 'your_cloudflare_api_key'
EMAIL = 'your_email'
DOMAINS_TO_UPDATE = [
    {
        'zone_id': 'zone_id_1',
        'domain': 'subdomain1.example.com',
        'proxied': True
    },
    {
        'zone_id': 'zone_id_1',
        'domain': 'subdomain2.example.com',
        'proxied': False
    },
    {
        'zone_id': 'zone_id_2',
        'domain': 'subdomain.example.org',
        'proxied': True
    }
]
```

## Usage
Run the script:

```
python update_dns.py
```

## Docker Deployment
Build the Docker container:

```
docker build -t dns-updater .
```

Run the Docker container:
```
docker run -d --name dns-updater --restart unless-stopped dns-updater
```

This will run the container in detached mode and ensure it starts automatically when the server restarts, unless you explicitly stop it.

### Docker Compose
You could also use docker-compose to build the project, with a local image or by pulling an external image. (modify to docker-compose.yml if you want to pull from an external image). The script in the container will use the code configuration or the environment variables, depending on whether the script is configured to use environment variables.
To build and run the image as a container run `docker compose up` (or `docker compose up -d` to run it detached as a background process).

## Tutorial
[Here](https://blog.devgenius.io/dns-updater-a-solution-for-managing-dynamic-ips-with-cloudflare-31be2f85d9fb) is a guide that shows you how to get the API Keys on cloudflare and how to set up this tool.

https://blog.devgenius.io/dns-updater-a-solution-for-managing-dynamic-ips-with-cloudflare-31be2f85d9fb
