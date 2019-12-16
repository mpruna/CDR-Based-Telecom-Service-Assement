In this project, I will propose a monitoring solution for Telecom services based on CDRs. CDRs or otherwise call detail records to hold specific information for traffic such as VoIP, Data, SMS. This event-driven solution can be used to monitor network service status proactively. We expect that at any given point, the data type should fall under specific values, and have a particular volume. For example, packet loss at any given time should be <1 %. The state of the network services is a sum based on a cumulative formula. These are "datapoint/point-features."
Will focus on:

    EPC SMS/DATA Traffic
    VoIP Traffic At the most simplistic level to ensure proper network operation, we must certain percentage of traffic is successful. In regular network operations, we can expect that a certain percentage of traffic is unsuccessful. When levels fall under a % threshold, a notification is sent.

Architecture Design

Under construction, for the time being, will use a simple compose file, but the plan is to create an elk-stack service in the cloud, either AWS/DigitalOcean. Elasticsearch DB with Kibana FE
Create a DATA blob sample

Based on a small data sample will create a bigger dataset using sample points.

    Dataset will be created using scikit learn library
    Data will thread based on regular daily traffic with an expect increased till mid-day
    We can use data_sample.csv for datapoints
    The other relevant info will be created to match the datapoint in a one-to-one relation, and distribution will be created based on the desired percentage. For instance, 80% of SMS will be MO
