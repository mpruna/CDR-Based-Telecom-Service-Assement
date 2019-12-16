![IMG](Images/Voip_Qos.png)


In this project, I will propose a monitoring solution for Telecom services based on CDRs. CDRs or otherwise call detail records to hold specific information for traffic such as VoIP, Data, SMS. This event-driven solution can be used to monitor network service status proactively. We expect that at any given point, the data type should fall under specific values, and have a particular volume. For example, packet loss at any given time should be <1 %. The state of the network services is a sum based on a cumulative formula. These are "datapoint/point-features."
Will focus on:

    EPC SMS/DATA Traffic
    VoIP Traffic At the most simplistic level to ensure proper network operation, we must certain percentage of traffic is successful. In regular network operations, we can expect that a certain percentage of traffic is unsuccessful. When levels fall under a % threshold, a notification is sent.

Architecture Design

We use Elastic stack components to set up the infrastructure. Each component executes a specific task below we can see a breakdown.

![IMG](Images/elk_stack.png)

Stack is deployed based on deployment.yml file. Within this file we define each service, number of replicas, failure scenario, ports, volumes etc. The same file can be used to deploy the stack locally with docker-compose.
Within project structure we define each component and it's functionality:

Component | Description
---|---|
Filebeat | lightweight process that ships log data
Logstash | Aggregation/Mediation layer
Elasticsearch | Nosql DB/Backend where we store the data
Kibana | Web gui

### Project Structure

```buildoutcfg
docker_admin@docker-elk1-us:~$ tree
.
├── docker-compose_stash.yml
├── filebeat
│   └── config
│       ├── filebeat.yml
├── get-docker.sh
├── kibana
│   └── kibana.yml
├── logstash
│   └── config
│       ├── logstash.conf
│      
└── sample_data
    ├── sms/
    └── voip/
8 directories, 5727 files
```


Based on a small data sample will create a bigger dataset using sample points.

    Dataset will be created using scikit learn library
    Data will thread based on regular daily traffic with an expect increased till mid-day
    We can use data_sample.csv for datapoints
    The other relevant info will be created to match the datapoint in a one-to-one relation, and distribution will be created based on the desired percentage. For instance, 80% of SMS will be MO
