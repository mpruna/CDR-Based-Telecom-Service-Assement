![IMG](Images/Voip/Voip_Qos.png)


In this project, I will propose a monitoring solution for Telecom services based on CDRs.
CDRs or otherwise call detail records to hold specific information for traffic such as **VoIP, Data, SMS**. 

This event-driven solution could be used to monitor network service status proactively. 
We expect that at any given point, a specific data type should fall under particular values. 
For instance, **VoIP Established session 99%, Max Jitter: 30ms, packet loss at any given time should be <1 %**.  
We can't expect the same traffic pattern at 23:00 or 10:00. The state of the network services is a sum based on a cumulative formula. These are "datapoint/point-features." Will focus on:

* EPC SMS/DATA Traffic
* VoIP Traffic 

### Architecture Design

We use Elastic stack components to set up the infrastructure. Each component executes a specific task below we can see a breakdown.

![IMG](Images/elk_stack.png)

The stack is deployed based on 'deployment.yml' file. Within this file, we define each **service, number of replicas, failure scenario, ports, volumes, etc**.

Component | Description
---|---|
Filebeat | lightweight process that ships log data
Logstash | Aggregation/Mediation layer
Elasticsearch | Nosql DB/Backend where we store the data
Kibana | Web gui

### Project Structure

```
├── docker-compose_stash.yml
├── get-docker.sh
├── Images
│   ├── docker_elkstack.png
│   ├── droppelets.png
│   ├── elk_stack.png
│   ├── SMS
│   │   ├── sms_dashboard.png
│   │   ├── sms_index.png
│   │   ├── sms_traffic_patterns.PNG
│   │   └── time_analysis.png
│   ├── sms_classification.PNG
│   ├── traffic_lan.png
│   ├── Voip
│   │   ├── SMS_Dashboard.png
│   │   ├── Voip_index.png
│   │   ├── Voip_Main.png
│   │   ├── Voip_Qos.png
│   │   ├── Voip Session Setup.png
│   │   └── Voip Trunk Traffic.png
│   └── Voip_Classification.PNG
├── Infrastructure
│   ├── docker-compose_stash.yml
│   ├── filebeat
│   │   ├── config
│   │   │   ├── filebeat.yml
│   │   │   └── filebeat.yml.bkp
│   │   └── Dockerfile
│   ├── get-docker.sh
│   ├── kibana
│   │   └── kibana.yml
│   ├── logstash
│   │   └── config
│   │       ├── logstash.conf
│   │       ├── logstash.conf.bkp
│   │       └── logstash_sms.conf
│   └── sample_data
│       ├── sms/
│       └── voip/
└── README.md

```


Based on a small data sample I created a bigger dataset.

* I used [scikit](https://scikit-learn.org/) learn library for data creation.
* Data will trend based on regular daily traffic with an expect increased till mid-day.
* We can use data_sample.csv for datapoints.
* The other relevant info will is generated to match the datapoint in a one-to-one relation, and distribution will be created based on the desired percentage. For instance, 80% of SMS will be MO.