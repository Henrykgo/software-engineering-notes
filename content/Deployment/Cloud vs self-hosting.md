The first deployment decision: run your system on hardware you own and operate (self-hosting/ on-premises) or using infrastructure provided by a third party (cloud service).


### Cloud
- **+** **Less operational burden**: the provider handles infrastructure setup and basic system administration, freeing the team to focus on the application. See [[Operations in the cloud]]
- **+** **Faster to get started**: much quicker than learning to deploy and operate the system yourself. 
- **+** **Provider expertise**: serving 1000s of customers, the provider has a lot of experience and may operate the system better than you could
- **Elasticity**: scale resources up and down with demand and pay only while you use them, instead of leaving them unused. See [[Cost]] and [[Scalability]]. For example: a large analytical query can temporarily use many machines in parallel and release them once the query is finished.

- **-** If **lacking a feature**: you need all you can do is ask the vender if they could add it; you generally cannot implement it yourself.
- **-** **Depends on their availability:** as when server is down all you can do is wait for it to recover.
- **-** **hard to debug**: as you generally cannot access the provider's server logs or internal performance data, making bugs and performance problems harder to diagnose
- **-**: **Vendor lock-in**: if a provider shuts down, raises prices, or changes the service, you have have to migrate. Lack of compatible APIs can make switching difficult and expensive. 
- **-**: **Political risk**: If the provider is in another country, political conflicts or sanctions could prevent access to the server.
- **-**: **Trust & Privacy**: Trust provider to keep the data secure, which can make privacy and regulatory compliance more complicated.

### Self-hosting






Cloud wins when load is unpredictable, you're small, or you're moving fast.
Self-hosting wins when load is large and steady, or when regulation demands control over where data lives. Many companies land on a hybrid of both.

Choosing the cloud is only the start: systems are designed to exploit its properties, rather than just running it is [[Cloud-native architecture]]

