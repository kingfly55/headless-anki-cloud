Title: 🔨 OpenAPI Tool Servers | Open WebUI

URL Source: https://docs.openwebui.com/openapi-servers/

Markdown Content:
Sponsored by Warp

[![Image 1: Warp](https://docs.openwebui.com/sponsors/banners/warp-banner.png)![Image 2: Warp](https://docs.openwebui.com/sponsors/banners/warp-banner-mobile.png)](https://warp.dev/open-webui)

The intelligent terminal for developers

This repository provides reference OpenAPI Tool Server implementations making it easy and secure for developers to integrate external tooling and data sources into LLM agents and workflows. Designed for maximum ease of use and minimal learning curve, these implementations utilize the widely adopted and battle-tested [OpenAPI specification](https://www.openapis.org/) as the standard protocol.

By leveraging OpenAPI, we eliminate the need for a proprietary or unfamiliar communication protocol, ensuring you can quickly and confidently build or integrate servers. This means less time spent figuring out custom interfaces and more time building powerful tools that enhance your AI applications.

☝️ Why OpenAPI?[​](https://docs.openwebui.com/openapi-servers/#%EF%B8%8F-why-openapi "Direct link to ☝️ Why OpenAPI?")
----------------------------------------------------------------------------------------------------------------------

*   **Established Standard**: OpenAPI is a widely used, production-proven API standard backed by thousands of tools, companies, and communities.

*   **No Reinventing the Wheel**: No additional documentation or proprietary spec confusion. If you build REST APIs or use OpenAPI today, you're already set.

*   **Easy Integration & Hosting**: Deploy your tool servers externally or locally without vendor lock-in or complex configurations.

*   **Strong Security Focus**: Built around HTTP/REST APIs, OpenAPI inherently supports widely used, secure communication methods including HTTPS and well-proven authentication standards (OAuth, JWT, API Keys).

*   **Future-Friendly & Stable**: Unlike less mature or experimental protocols, OpenAPI promises reliability, stability, and long-term community support.

🚀 Quickstart[​](https://docs.openwebui.com/openapi-servers/#-quickstart "Direct link to 🚀 Quickstart")
--------------------------------------------------------------------------------------------------------

Get started quickly with our reference FastAPI-based implementations provided in the `servers/` directory. (You can adapt these examples into your preferred stack as needed, such as using [FastAPI](https://fastapi.tiangolo.com/), [FastOpenAPI](https://github.com/mr-fatalyst/fastopenapi) or any other OpenAPI-compatible library):

`git clone https://github.com/open-webui/openapi-serverscd openapi-servers`

### With Bash[​](https://docs.openwebui.com/openapi-servers/#with-bash "Direct link to With Bash")

`# Example: Installing dependencies for a specific server 'filesystem'cd servers/filesystempip install -r requirements.txtuvicorn main:app --host 0.0.0.0 --reload`

The filesystem server should be reachable from: [http://localhost:8000](http://localhost:8000/)

The documentation path will be: [http://localhost:8000](http://localhost:8000/)

### With Docker[​](https://docs.openwebui.com/openapi-servers/#with-docker "Direct link to With Docker")

If you have docker compose installed, bring the servers up with:

`docker compose up`

The services will be reachable from:

*   [Filesystem localhost:8081](http://localhost:8081/)
*   [memory server localhost:8082](http://localhost:8082/)
*   [time-server localhost:8083](http://localhost:8083/)

Now, simply point your OpenAPI-compatible clients or AI agents to your local or publicly deployed URL—no configuration headaches, no complicated transports.

*   For general discussions, technical exchange, and announcements, visit our [Community Discussions](https://github.com/open-webui/openapi-servers/discussions) page.
*   Have ideas or feedback? Please open an issue!
