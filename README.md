
# Edge-to-Cloud Agentic AI for Preventive Maintenance
## Deployment Model of Cloud to Local Site

This README details the deployment plans for a scalable, cloud-integrated architecture of an autonomous agentic AI service across multiple factory locations to perform predictive and preventive maintenance. 

## Overview
This diagram supports a cloud-based, autonomous agentic AI service acting through Azure tools to be deployed on factory IPCs running a Kubernetes cluster, utilizing the factory's Edge Sensors in real-time with the locally-acting agentic AI to notify the factory of potential non-scheduled maintenance needs. The expected outcome will be a reduction in maintenance issues and costs, reduced downtime, and reduced safety issues.

## Architecture Diagram for Agentic AI for Preventive Maintenance Use Case

CLOUD LAYER
``` 

└── Azure Machine Learning
    └── Trains and versions the central AI model
    └── Publishes model containers to Azure Container Registry (ACR)

└── Azure Container Registry (ACR)
    └── Stores versioned containers (AI service, logic, configs)

└── Azure Arc
    └── Connects to each factory’s on-site Kubernetes cluster
    └── Deploys AI containers to registered edge locations

└── Azure Monitor / Log Analytics
    └── Collects performance metrics from edge clusters
    └── Tracks uptime, inference success, error rates

└── Central AI Dashboard (VP of Maintenance)
    └── Aggregates reports + metrics from all sites
    └── Displays trends, cost savings, and maintenance wins
``` 

FACTORY / EDGE LAYER (per site)
``` 
└── Industrial PC (IPC) running Kubernetes
    └── Hosts the AI agent container (deployed via Arc)
    └── Collects data from factory sensors and machines
└── Edge Sensors
    └── Provide live inputs (temperature, vibration, etc.)

└── Local AI Agent
    └── Analyzes inputs in real time
    └── Triggers alerts or maintenance actions
    └── Sends reports on activity and outcomes

└── Plant Manager / Maintenance Lead
    └── Responds to actionable local notifications
```


DATA FLOW
1. AI model trained → published to Azure Arc (ACR)
2. Azure Arc pushes container → deployed to factory Kubernetes clusters
3. Local AI makes decisions → alerts plant staff + logs activity
4. Summary reports and metrics sync to cloud
5. Central dashboard provides unified insights to Corp 

---

## Cloud Architecture

- **Azure Machine Learning**: Trains and versions preventive maintenance models.
- **Azure Container Registry (ACR)**: Hosts versioned containers for deployment.
- **Azure Arc**: Connects and manages remote Kubernetes clusters at factory sites.
- **Azure Monitor**: Collects performance logs and metrics from local deployments.
- **Central AI Dashboard**: Consolidates reports for executive visibility.

---

## Edge Architecture (Per Factory)

- **Industrial PC (IPC)**: Hosts a Kubernetes cluster for containerized workloads.
- **Edge Sensors**: Provide real-time equipment telemetry.
- **Local AI Agent**: Processes sensor data and triggers maintenance alerts/actions.
- **Plant Managers**: Respond to AI-triggered actions and verify resolutions.

---

## Data Flow

1. Central AI model → Published to Azure Container Registry.
2. Azure Arc pushes containers → Edge IPCs running Kubernetes.
3. AI agents at the edge trigger alerts locally.
4. Reports and metrics stream back to Azure.
5. Dashboard displays performance, trends, and cost savings.

---

## Glossary

- **Azure Arc**: Extends Azure management to on-prem and multi-cloud environments.
- **Edge AI**: AI that operates locally near the data source.
- **Agentic AI**: Autonomous, goal-directed AI systems.
- **Kubernetes Cluster**: Container orchestration system managing deployment and scaling.
- **Industrial PC (IPC)**: Rugged local compute node near factory equipment.

---

## Deployment Example

```bash
# Tag and push the AI container
docker tag maintenance-ai:v1 myacr.azurecr.io/maintenance-ai:v1
docker push myacr.azurecr.io/maintenance-ai:v1

# Deploy container to remote factory site via Azure Arc
az connectedk8s proxy -n factory-site-cluster
kubectl apply -f maintenance-ai-deployment.yaml
```

---

## Next in line to design:

1. Build Out the Cloud Architecture.  
2. Define the Edge Stack in Detail.  
3. Create a Sample Use Case for the AI Model.  
4. Create a Pitch Deck.  


## Outcome

This architecture enables:
- Real-time predictive maintenance
- Reduced downtime and repair costs
- Cloud-driven oversight without compromising edge autonomy
- Scalable deployment across factory networks

## Related Microsoft Docs

- [Azure Machine Learning](https://learn.microsoft.com/en-us/azure/machine-learning/)
- [Azure Arc](https://learn.microsoft.com/en-us/azure/azure-arc/)
- [Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/)
- [Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/)

---

---

## Contributors

- **Solution Owner**: Carol Setters
- **Architecture Support**: ChatGPT (OpenAI)
