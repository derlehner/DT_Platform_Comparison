# Digital Twin Platforms: Current Capabilities andFuture Prospects

## Evaluation

### Microsoft Azure
From Microsoft Azure, we considered the [Azure Digital Twins Service](https://azure.microsoft.com/services/digital-twins/) as main component of the provided DT platform. Based on the documentation of this service, it is recommended to use [Azure IoT-Hub](https://azure.microsoft.com/services/iot-hub/)  [to send data from devices](https://docs.microsoft.com/en-us/azure/digital-twins/tutorial-end-to-end), and connect the Azure Digital Twins Service to the [Azure Time Series Insights Service](https://azure.microsoft.com/services/time-series-insights/) for [analysis of historical data](https://docs.microsoft.com/en-us/azure/time-series-insights/tutorials-model-sync). Therefore, we also integrated these two services into our comparison for Azure.
#### Compatibility

##### Platform Interoperability 
The Azure DT Platform offers a REST-Interface
##### System Interoperability 
Enabled via the IoT-Hub, and specified via so-called Relationships between different Digital Twins

##### Automation Protocols
Based on the official [documentation](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-protocols), the Azure IoT-Hub currently supports the following communication protocols:
- MQTT
- AMQP
- HTTPS
### Security
#### Connection Security
Authorization via [Azure Active Directory](https://azure.microsoft.com/de-de/services/active-directory/)
https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-security for Devices and https://docs.microsoft.com/en-us/azure/digital-twins/concepts-security for Azure DT
#### Data Security
Send data to platform: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md https://docs.microsoft.com/en-us/security/benchmark/azure/baselines/iot-hub-security-baseline
Transporting data within platform (event hubs): https://techcommunity.microsoft.com/t5/messaging-on-azure/data-encryption-with-customer-managed-keys-for-azure-event-hubs/ba-p/839122
Stored data (in ADT and TSI): https://docs.microsoft.com/en-us/azure/digital-twins/concepts-security#encryption-of-data-at-rest and azure data store used by TSI: https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption


#### Portability

##### CI/CD

As to the best of our knowledge, there is yet no support for either CI or CD by any of the components of the azure digital twin platform.

#### Maintainability

##### Modifiability 

##### Reusability
As the Digital Twin Definition Language (DTDL) used by Microsoft Azure Digital Twins to describe components is [JSON-LD-based](https://docs.microsoft.com/en-us/azure/digital-twins/concepts-models), this allows easy reusability using copy and paste of json properties.

#### Performance

##### Real-Time Behavior
https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/realtime-analytics-vehicle-iot

##### Functional Suitability

#### Compatibility

##### Platform Interoperability 

##### Bi-Directional Synchronization 

##### Verify & Validate

##### Convergence

#### Usability

##### Language Support 
Both Azure and Eclipse Vorto provide a structured meta-model (DTDL\footnote{\url{https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md}} and vortolang\footnote{\url{https://github.com/eclipse/vorto/blob/development/docs/vortolang-1.0.md}} that can be instantiated with specific DT models using json. Both also provide modeling tools (ADT-Explorer\footnote{\url{https://docs.microsoft.com/en-us/samples/azure-samples/digital-twins-explorer/digital-twins-explorer}} and Vorto Repository\footnote{\url{https://vorto.eclipseprojects.io/}}

##### Visualization of DTs
https://github.com/eclipse/vorto/blob/master/docs/tutorials/create_webapp_dashboard.md
### Eclipse 
For the Eclipse platform, we analyzed the Hono, Ditto and Vorto tools that all claim to provide solutions to cope with Digital Twins.
#### Compatibility

##### Platform Interoperability 
Main functionality of Ditto is to provide a RESTful Interface to enable platform interopability. Therefore, this requirement is fulfilled by this platform.
##### System Interoperability 
In the officiall documentation of the structure that is used behind the platform, there is no support for interaction between different Digital Twins. However, this could still be implemented, as Hono offers different. For the authors, this leads to the conclusion that system interopability is partially fulfilled by the platform.

##### Automation Protocols
Based on the Eclipse Hono Website, there is a out of the box support for the following protocols to send data from a device to the platform:
- HTTP
- AMQP
- MQTT
- CoAP

### Security
#### Connection Security

Hono: https://www.eclipse.org/hono/docs/architecture/auth/
Eclipse: via Accounts in Vorto Repository
Ditto: via Authentication/Authorization https://www.eclipse.org/ditto/basic-auth.html#authentication and Access Rights via Policy Concept: https://www.eclipse.org/ditto/basic-policy.html#model-specification

#### Data Security

Sending data to platform: https://www.eclipse.org/hono/docs/admin-guide/secure_communication/ 
Storing data in platform: https://www.eclipse.org/ditto/connectivity-tls-certificates.html

#### Portability

##### CI/CD
As to the best of our knowledge, there is no out of the box support for CI or CD by Eclipse Hono, Ditto or Vorto.

#### Maintainability

##### Modifiability 
The[ REST API offered by Eclipse Ditto](https://www.eclipse.org/ditto/http-api-doc.html) allows the modification of the system and its components during runtime.
##### Reusability
The [Vorto Repository] allows the persistance, publication and re-using of existing models that describe hardware components.
#### Performance

##### Real-Time Behavior
via MQTT https://www.eclipse.org/hono/docs/user-guide/mqtt-adapter/ and AMQP https://www.eclipse.org/hono/docs/user-guide/amqp-adapter/ adapters

##### Functional Suitability

#### Compatibility

##### Bi-Directional Synchronization 

##### Verify & Validate

##### Convergence

#### Usability

##### Modeling Support 

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

##### CI/CD

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



