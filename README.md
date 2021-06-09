# Our Title here



## Evaluation

### Amazon Greengrass

#### Compatibility

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





