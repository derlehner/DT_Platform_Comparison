# Digital Twin Platforms: Current Capabilities and Future Prospects

## Evaluation

### Microsoft Azure
From Microsoft Azure, we considered the [Azure Digital Twins (ADT) Service](https://azure.microsoft.com/services/digital-twins/) as main component of the provided DT platform. Based on the documentation of this service, it is recommended to use [Azure IoT-Hub](https://azure.microsoft.com/services/iot-hub/)  [to send data from devices](https://docs.microsoft.com/en-us/azure/digital-twins/tutorial-end-to-end), and connect the Azure Digital Twins Service to the [Azure Time Series Insights Service](https://azure.microsoft.com/services/time-series-insights/) for [analysis of historical data](https://docs.microsoft.com/en-us/azure/time-series-insights/tutorials-model-sync). Therefore, we also integrated these two services into our comparison for Azure.
#### Compatibility

##### Platform Interoperability 
The Azure DT Platform offers a [REST-Interface](https://docs.microsoft.com/en-us/rest/api/azure-digitaltwins/) that allows both the retrieving of data/structural information, and communicating with a DT (i.e. sending data, or updating its structure). As a result, this requirement is fully fulfilled.
##### System Interoperability 
This requirement is partially fulfilled, as the modeling of relationships in the [Digital Twin Definition Language (DTDL)](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md) used by the ADT service, but there is no dedicated support for implementing connections between physical devices based on these modeled relationships.

##### Automation Protocols
Based on the official [documentation](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-protocols), the Azure IoT-Hub currently supports the following communication protocols:
- MQTT
- AMQP
- HTTPS
This means that none of the defined automation protocols is supported, resulting in the requirement Automation Protocols being not fulfilled.
### Security
Data security is provided for all considered tools.
- For sending data to the platform: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md https://docs.microsoft.com/en-us/security/benchmark/azure/baselines/iot-hub-security-baseline
- For transporting data within platforms (via event hubs): https://techcommunity.microsoft.com/t5/messaging-on-azure/data-encryption-with-customer-managed-keys-for-azure-event-hubs/ba-p/839122
- For data stored in the ADT service: https://docs.microsoft.com/en-us/azure/digital-twins/concepts-security#encryption-of-data-at-rest
- For the azure data store used by Time Series Insights: https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption
Connection security is provided for all considered tools via the [Azure Active Directory](https://azure.microsoft.com/de-de/services/active-directory/).
More information on connection security is also provided by azure [for device communication with IoT-Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-security) and for the [ADT-service](https://docs.microsoft.com/en-us/azure/digital-twins/concepts-security)


#### Portability

##### Continuous Integration & Continuous Development (CI/CD)
The Azure [DevOps Services](https://azure.microsoft.com/pricing/details/devops/azure-devops-services/) provide dedicated CI/CD support via so-called [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines/). There is also [documentation](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/apps/devops-dotnet-webapp) provided on how to use this tooling. as a result, this requirement is fulfilled.

##### Portability
As all investigated tools are cloud-native in nature, but there is also an option for standalone deployment, this requirement is fulfilled.
#### Maintainability

##### Modifiability 
The REST API provided by the ADT service [offers operations that allow to change DTs and their properties](https://docs.microsoft.com/en-us/rest/api/digital-twins/controlplane/endpoints), also during runtime of the actual system. Therefore, this requirement is fulfilled.

##### Reusability
As the Digital Twin Definition Language (DTDL) used by Microsoft Azure Digital Twins to describe components is [JSON-LD-based](https://docs.microsoft.com/en-us/azure/digital-twins/concepts-models), this allows easy reusability using copy and paste of json properties. As this is also possible between projects, this requirement is fulfilled.

#### Performance

##### Real-Time Behavior
There is some information on how data can be transported to the IoT-Hub in real-time https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/realtime-analytics-vehicle-iot. However, current technical limitations do not allow to provide real-time support to the cloud, where the actual DT is running in the ADT service. Therefore, this requirement is partially fulfilled.

#### Functional Suitability

##### Bi-Directional Synchronization 
The bi-directional synchronization can be achieved via the IoT-Hub. However, our experiments showed that for actually implementing this, limited support is provided, because the code for synchronization must be created manually. Thus, this requirement is partially fulfilled.

##### Verify & Validate
Our experiments showed that the ADT service automatically detects invalid structures during runtime, but to the best of our knowledge, there is no support by the Azure platform to run test cases before the deployment of a DT. As a result, this requirements is partially fulfilled.
##### Convergence
As to the best ouf our knowledge, there is yet no dedicated support by the Azure platform for Convergence. Therefore, this requirement is not fulfilled.

#### Usability

##### Language Support 
The [Digital Twin Definition Language(DTDL](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md) is a dedicated language offered by Microsoft to model Digital Twins in the ADT service. A graphical interface for this language is provided by the [ADT-Explorer](https://docs.microsoft.com/en-us/samples/azure-samples/digital-twins-explorer/digital-twins-explorer)

### Eclipse 
For the Eclipse platform, we analyzed the [Hono](https://www.eclipse.org/hono), [Ditto](https://www.eclipse.org/ditto/) and [Vorto](https://www.eclipse.org/vorto/) tools that all claim to provide solutions to cope with Digital Twins, and for which there is also an [integration example for a specific use case](https://blog.bosch-si.com/developer/harmonizing-specific-device-payloads-using-eclipse-vorto/) provided by eclipse.
#### Compatibility

##### Platform Interoperability 
The main functionality of Ditto is to provide a [RESTful Interface to enable platform interopability](https://www.eclipse.org/ditto/http-api-doc.html).  Therefore, this requirement is fulfilled by this platform.
##### System Interoperability 
In the [officiall documentation of the structure that is used behind the platform](https://github.com/eclipse/vorto/blob/development/docs/vortolang-1.0.md), there is no support for interaction between different Digital Twins. Therefore, System Interopability is not fulfilled by this platform.

##### Automation Protocols
Based on the Eclipse Hono Website, there is a out of the box support for the following protocols to send data from a device to the platform:
- HTTP
- AMQP
- MQTT
- CoAP

This means that none of the defined automation protocols is supported, resulting in the requirement Automation Protocols being not fulfilled.
### Security
Connection Security is enabled in
-  Hono: https://www.eclipse.org/hono/docs/architecture/auth/
- Vorto: via Accounts in [Vorto Repository](https://vorto.eclipseprojects.io/)
- Ditto: via Authentication/Authorization https://www.eclipse.org/ditto/basic-auth.html#authentication and Access Rights via Policy Concept: https://www.eclipse.org/ditto/basic-policy.html#model-specification

Data Security is enabled for
- Sending data to platform: https://www.eclipse.org/hono/docs/admin-guide/secure_communication/ 
- Storing data in platform: https://www.eclipse.org/ditto/connectivity-tls-certificates.html

Therefore, Security is fulfilled by this platform.

#### Portability

##### Continuous Integration & Continuous Development (CI/CD)
As to the best of our knowledge, there is no out of the box support for CI or CD by Eclipse Hono, Ditto or Vorto. As a result, this requirement is not fulfilled.
##### Provisioning
This requirement is partly fulfilled, as the individual tools can be hosted on-premise, but there is no cloud-native solution for them.

#### Maintainability

##### Modifiability 
The [REST API offered by Eclipse Ditto](https://www.eclipse.org/ditto/http-api-doc.html) allows the modification of the system and its components during runtime, via dedicated POST/PUT/DELETE operations for the individual components of a Digital Twin. As a result, this requirement is fully fulfilled.
##### Reusability
The [Vorto Repository] allows the persistance, publication and re-using of existing models that describe hardware components. As this re-usability is also possible across projects, this requirement is fulfilled.
#### Performance

##### Real-Time Behavior
Real-Time behavior can be achieved on the edge via an MQTT https://www.eclipse.org/hono/docs/user-guide/mqtt-adapter/ or AMQP https://www.eclipse.org/hono/docs/user-guide/amqp-adapter/ adapter. However, current technical limitations do not allow real-time behavior over the cloud. Therefore, this requirement is partially fulfilled.

#### Functional Suitability

##### Bi-Directional Synchronization 
The bi-directional synchronization can be achieved via Eclipse HOno. However, our experiments showed that for actually implementing this, limited support is provided, because the code for synchronization must be created manually.

##### Verify & Validate
Our experiments showed that the Eclipse platform does not detect invalid structures during runtime, and to the best of our knowledge, there is no support by the Eclipse platform to run test cases before the deployment of a DT. As a result, this requirements is not fulfilled.
##### Convergence
As to the best ouf our knowledge, there is yet no dedicated support by any of the investigated tools for Convergence. Therefore, this requirement is not fulfilled.
#### Usability

##### Language Support 
The [Vortolang](https://github.com/eclipse/vorto/blob/development/docs/vortolang-1.0.md) is a dedicated language offered by Eclipse Vorto to model Digital Twins in the ADT service. A graphical interface for this language is provided by the [Vorto Repository](https://vorto.eclipseprojects.io)
Therefore, this requirement is fulfilled.

### Amazon Greengrass

#### Compatibility

##### Platform Interoperability 

AWS IoT Greengrass provides [Greengrass Connectors](https://docs.aws.amazon.com/greengrass/v1/developerguide/connectors.html) to connect to other services, protocols, local infrastructure, AWS, and even third-party cloud services. Thus, we consider this requirement as fulfilled.

##### System Interoperability 

Since communication in AWS IoT Greengrass is mostly handled via MQTT digital twins can interact with each other via this protocol. Communication is possible, both locally between digital twins of devices, and via the AWS IoT Core, running in the cloud (see [Interacting with devices in an IoT Greengrass Group](https://docs.aws.amazon.com/greengrass/v1/developerguide/module4.html)). Via [connectors](https://docs.aws.amazon.com/greengrass/v1/developerguide/connectors.html), it is also possible to interact with digital twins outside of AWS. Despite the connection is automatically established, the communication itself has to be defined manually. Thus, we consider this requirement partially fulfilled.

##### Automation Protocols 

https://docs.aws.amazon.com/iot-sitewise/latest/userguide/industrial-data-ingestion.html

AWS IoT SiteWise consumes industrial data and matches data to assets that represent your industrial operations. AWS IoT SiteWise supports linking with OPC-UA, Modbus TCP, and Ethernet/IP protocols.

### Security

#### Connection & Data Security

AWS provides a variety of security mechanisms (see [Overview of AWS IoT Greengrass Security](https://docs.aws.amazon.com/greengrass/v1/developerguide/gg-sec.html)). For the connection between the device, AWS IoT Core, and the AWS cloud, AWS employs key pairs and certificates for authentication and policies for authorization (see [Authentication and Authorization for AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/v1/developerguide/device-auth.html). For users interacting with AWS IoT Greengrass resources, AWS provides [IAM](https://docs.aws.amazon.com/greengrass/v1/developerguide/security-iam.html) that enables administrators to control access to the different resources. 

AWS uses [Transport Layer Security (TLS)](https://docs.aws.amazon.com/greengrass/v1/developerguide/encryption-in-transit.html) to encrypt all communication that is sent to or from the AWS cloud using MQTT or HTTPS protocols. Further Data security measures by AWS can be looked up [here](https://docs.aws.amazon.com/greengrass/v1/developerguide/data-encryption.html). 

Consequently, we consider the security requirement as fulfilled by AWS.

#### Portability

##### Continuous Integration & Continuous Development (CI/CD)

AWS offers full [CI/CD](https://aws.amazon.com/de/blogs/iot/implementing-a-ci-cd-pipeline-for-aws-iot-greengrass-projects/) support. For instance, a developer could push code to an AWS git repository, this triggers the AWS CodePipeline, that uses AWS CodeBuild. CodeBuild could perform the following tasks:

1. Deploy the changes to an IoT Greengrass test group
2. Execute tests
3. After successful test results, deploy the changes to a production IoT Greengrass group to make the changes available to users.

Hence, we consider the CI/CD requirement as fulfilled. 

#### Maintainability

##### Modifiability 

In AWS IoT Greengrass Developers can change or replace deployed services, or functionalities via [IoT Greengrass Groups](https://docs.aws.amazon.com/greengrass/v1/developerguide/deployments.html). They enable you to organize the deployment of your digital twin instance. There you can assign the different entities of AWS IoT Greengrass, among others, devices, lambda functions, connectors, subscriptions, to a group, organize, control, and define dependencies and relationships between them. Furthermore, it is possible to exchange and redeploy all entities. This can be done manually via the AWS console or terminal, or via a CI/CD pipeline. However, this is not possible during runtime. Hence, this requirement is only partially fulfilled.

##### Reusability

AWS IoT Greengrass [components](https://docs.aws.amazon.com/greengrass/v2/developerguide/manage-components.html) enable to deploy software modules to Greengrass core devices. Components can represent applications, runtime installers, libraries, or any other kind of code you would want to run on your core devices. Components can be defined and depend on other components. These components can be tested and developed locally on your core device. When the component is ready to be deployed, it can be uploaded to AWS IoT Greengrass in the AWS cloud and be reused in other groups or devices. AWS IoT Greengrass also provides pre-built components that users can reuse in their applications. For instance, a pre-built component lets you publish data to [Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) for measuring the performance of your system.

Because AWS IoT Greengrass provides the concept of reusable components and even offers pre-built components itself, we consider the requirement of reusability as fulfilled.

#### Performance

##### Time Behavior

With [FreeRTOS](https://aws.amazon.com/freertos/?nc1=h_ls) AWS provides a real-time operating system for microcontrollers running on edge devices. However, the data processed in real-time at the microcontroller is not communicated in real-time to the core device on the edge, or AWS IoT, running in the cloud. 

Thus, we consider this requirement to be partially fulfilled because AWS offers an OS to perform real-time processing, but the real-time is not ensured across other functionalities of AWS IoT Greengrass.

#### Functional Suitability

##### Bi-Directional Synchronization 

In AWS IoT Greengrass, the communication between edge and cloud bases on [MQTT and HTTPS](https://docs.aws.amazon.com/iot/latest/developerguide/protocols.html). The connection between AWS Greengrass, running on edge devices, and AWS IoT, running in the cloud, is established by downloading certificates and secrets right from the AWS console. However, the MQTT Topics and Subscriptions have to be created by hand, and also the messages send over MQTT have to be defined manually. With this, the software engineer has to ensure programmatically that at all times the digital twin is synchronized with its physical counterpart. Thus, we evaluated bi-directional synchronization as partially fulfilled in AWS IoT Greengrass.

##### Verify & Validate

AWS IoT Greengrass provides an [AWS IoT Device Tester](https://aws.amazon.com/de/greengrass/device-tester/) to perform test automation for connected Linux-based devices. The test suite verifies whether the AWS IOT Greengrass Core software runs on your hardware and can communicate with the AWS Cloud. It also performs end-to-end tests with the IoT Core running in the cloud, e.g., it verifies that your device can send and receive MQTT messages and process them correctly. Besides these predefined tests. It is also possible to perform your test cases (see [Use IDT to develop and run your test suites](https://docs.aws.amazon.com/greengrass/v1/developerguide/idt-custom-tests.html)). Because of this comprehensive testing environment, we consider the Verify & Validate requirement as fulfilled.

##### Convergence

AWS IoT Greengrass does not provide any support in achieving high convergence between the digital and the physical space. It is possible to achieve it programmatically but there is no out-of-the-box solution or guidelines from AWS itself on how to achieve convergence. Thus, we consider this requirement as not fulfilled.

#### Usability

##### Modeling Support 

AWS IoT Greengrass does not provide any modeling capabilities to represent data about physical devices, their types, and their data. Thus, modeling support is not available, and hence, not fulfilled.



