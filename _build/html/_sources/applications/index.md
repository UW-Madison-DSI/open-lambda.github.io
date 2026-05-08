# Applications

We are building OL to support a wide range of applications with minimal changes required from those applications. Our approach is to port more real-world workloads and let their needs drive incremental improvements to the platform.

## Want to deploy FastAPI apps on OpenLambda?  Just ASGI us how.

In this post, we look at an agricultural forecasting application and an ASGI-based web service. The ag app is a natural fit for serverless because it is fundamentally stateless: results can be regenerated on demand from underlying data rather than relying on persistent runtime state. This also influenced the choice of FastAPI for a modern, async-friendly interface.
To situate ASGI, it builds on the long history of WSGI-based Python web serving, where earlier work (including Jaime’s contributions) helped shape synchronous server patterns. ASGI extends this model with native async support, enabling higher concurrency and better I/O utilization, but requiring deeper runtime integration.
A broader design question is whether it is beneficial to consolidate multiple functions into a single Lambda-like unit. We believe it is: co-locating functions enables opportunistic state reuse, faster warm starts, and reduced overhead.
On the implementation side, OL removes its dependency on Tornado and adds optional support for both WSGI and ASGI applications. The ag forecasting app also surfaced practical issues, including /dev/shm constraints when using process pools, which required targeted adjustments.
Looking ahead, improved visibility into execution—such as detecting when applications are blocked on I/O—opens the door to new billing models that distinguish compute from idle waiting time, addressing a longstanding serverless concern.
More broadly, expanding the set of supported applications continues to drive OL’s evolution, alongside features like environment variables and GitHub-based deployments that further reduce friction for onboarding new workloads.

- [Ag Forecasting API](ag-forecasting-api.md) 