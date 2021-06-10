# Our Title here

## Discussion Points
- Welche Hierarchien haben wir? Sollen wir nach Requirements oder nach Plattformen strukturieren?

## Evaluation

### Microsoft Azure
From the Microsoft Azure, we considered the Azure Digital Twins Service, the Azure IoT-Hub, and the Azure Time Series Insights Service.
#### Compatibility

##### Platform Interoperability 
The Azure DT Platform offers a REST-Interface
##### System Interoperability 
Enabled via the IoT-Hub, and specified via so-called Relationships between different Digital Twins
##### Real-Time Busses 
As to the best of our knowledge, there is no support for real-time busses in Azure.

##### Automation Protocols
Based on the official [documentation](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-protocols), the Azure IoT-Hub currently supports the following communication protocols:
- MQTT
- AMQP
- HTTPS

#### Portability

##### CI/CD

#### Maintainability

##### Modifiability 

##### Reusability
As the Digital Twin Definition Language (DTDL) used by Microsoft Azure Digital Twins to describe components is [JSON-LD-based](https://docs.microsoft.com/en-us/azure/digital-twins/concepts-models), this allows easy reusability using copy and paste of json properties.

#### Performance

##### Time Behavior

##### Functional Suitability

#### Compatibility

##### Platform Interoperability 

##### Bi-Directional Synchronization 

##### Verify & Validate

##### Convergence

#### Usability

##### Modeling Support 
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
##### Real-Time Busses 
As to the best of our knowledge, there is no support for real-time busses in the examined Eclipse tools.

##### Automation Protocols
Based on the Eclipse Hono Website, there is a out of the box support for the following protocols to send data from a device to the platform:
- HTTP
- AMQP
- MQTT
- CoAP

#### Portability

##### CI/CD
As to the best of our knowledge, there is no out of the box support for CI or CD by Eclipse Hono, Ditto or Vorto.

#### Maintainability

##### Modifiability 
The[ REST API offered by Eclipse Ditto](https://www.eclipse.org/ditto/http-api-doc.html) allows the modification of the system and its components during runtime.
##### Reusability
The [Vorto Repository] allows the persistance, publication and re-using of existing models that describe hardware components.
#### Performance

##### Time Behavior

##### Functional Suitability

#### Compatibility

##### Bi-Directional Synchronization 

##### Verify & Validate

##### Convergence

#### Usability

##### Modeling Support 

### Amazon Greengrass

##### Platform Interoperability 

AWS IoT Greengrass provides [Greengrass Connectors](https://docs.aws.amazon.com/greengrass/v1/developerguide/connectors.html) to connect to other services, protocols, local infrastructure, AWS, and even third-party cloud services. Thus, we consider this requirement as fulfilled.

##### System Interoperability 

Since communication in AWS IoT Greengrass is mostly handled via MQTT it is possible for digital twins to interact with each other via this protocol. Communication is possible, both locally between digital twins of devices, and via the AWS IoT Core, running in the cloud (see [Interacting with devices in an IoT Greengrass Group](https://docs.aws.amazon.com/greengrass/v1/developerguide/module4.html)). Via [connectors](https://docs.aws.amazon.com/greengrass/v1/developerguide/connectors.html) it is also possible to interact with digital twins outside of AWS.  Thus, system interoperability is fulfilled.

##### Real-Time Busses 

##### Automation Protocols 

#### Portability

##### CI/CD

AWS offers full [CI/CD](https://aws.amazon.com/de/blogs/iot/implementing-a-ci-cd-pipeline-for-aws-iot-greengrass-projects/) support. For instance, a developer could push code to a AWS git repository, this triggers the AWS CodePipeline, that uses AWS CodeBuild. CodeBuild could perform the following tasks:

1. Deploy the changes to a IoT Greengrass test group
2. Execute tests
3. After successful test results, deploy the changes to a production IoT Greengrass group to make the changes available to users.

Hence, we consider the CI/CD requirement as fulfilled. 

#### Maintainability

##### Modifiability 

In AWS IoT Greengrass Developers can change or replace deployed services, or functionalities via [IoT Greengrass Groups](https://docs.aws.amazon.com/greengrass/v1/developerguide/deployments.html). They enable to organize the deployment of your digital twin instance. There you can assign the different entities of AWS IoT Greengrass, among others, devices, lambda functions, connectors, subscriptions, to a group, organize, control, and define dependencies and relationships between them. Furthermore, it is possible to exchange and redeploy all entities. This can be done manually via the AWS console or terminal, or via a CI/CD pipeline.

##### Reusability

AWS IoT Greengrass [components](https://docs.aws.amazon.com/greengrass/v2/developerguide/manage-components.html) enable to deploy software modules to Greengrass core devices. Components can represent applications, runtime installiers, libraries or any other kind of code you would want to run on your core devices. Components can be defined and depend on other components. These components can be tested and developed locally on your core device. When the component is ready to be deployed, it can be uploaded to AWS  IoT Greengrass in the AWS cloud and be reused in other groups or devices. AWS IoT Greengrass also provides pre-built components that users can reuse in their applications. For instance, a pre-built component lets you publish data to [Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) for measuring the performance of your system.

Because AWS IoT Greengrass provides the concept of reusable components, and even offers pre-built components itself, we consider the requirement of reusability as fulfilled.

#### Performance

##### Time Behavior

With [FreeRTOS](https://aws.amazon.com/freertos/?nc1=h_ls) AWS provides a real-time operating system for microcontrollers running on edge devices. However, the data processed in real-time at the microcontroller, is not communicated in real-time to the core device on the edge, or AWS IoT, running in the cloud. 

Thus, we consider this requirement to be partially-fulfilled, because AWS offers a OS to perform real-time processing, but the real-time is not ensured across other functionalities of AWS IoT Greengrass.

#### Functional Suitability

##### Bi-Directional Synchronization 

In AWS IoT Greengrass, the communication between edge and cloud bases on MQTT. The connection between AWS Greengrass, running on edge devices, and AWS IoT, running in the cloud, is established by downloading certificates and secrets right from the AWS console. However, the MQTT Topics and Subscriptions have to be created by hand and also the messages send over MQTT have to be defined manually. With this, the software engineer has to ensure programatically that at all time the digital twin is synchronized with its physical counterpart. Thus, we evaluated bi-directional synchronization as partially-fullfilled in AWS IoT Greengrass.

##### Verify & Validate

AWS IoT Greengrass provides a [AWS IoT Device Tester](https://aws.amazon.com/de/greengrass/device-tester/) to perform test automation for connected linux-based devices. The test suite verifies whether the AWS IOT Greengrass Core software runs on your hardware and can communicate with the AWS Cloud. It also performs end-to-end tests with the IoT Core running in the cloud, e.g., it verifies that your device can send and receive MQTT messages and process them correctly. Besides these predefined tests. It is also possible to perform own test cases (see [Use IDT to develop and run your own test suites](https://docs.aws.amazon.com/greengrass/v1/developerguide/idt-custom-tests.html)). Because of this comprehensive testing environment, we consider the Verify & Validate requirement as fulfilled.

##### Convergence

AWS IoT Greengrass does not provide any support in achieving high convergence between the digital and the physical space. It is possible to achieve it programatically but there is no out of the box solution or guidelines from AWS itself how to achieve convergence. Thus, we consider this requirement as not fulfilled.

#### Usability

##### Modeling Support 

AWS IoT Greengrass does not provide any modelling capabilities for represent data about physical devices, their types, and their data. Thus, modelling support is not available, and hence, not fulfilled.





