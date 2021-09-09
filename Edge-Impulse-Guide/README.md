# Introduction

Project 15 enable efforts to quickly get started with a foundation for a IoT solution. Devices can be provisioned and managed trough the P15 portal and it displays live events and telemetry as text as well as with Time Series Insights and on map.  

Added to the Open Platform is the integration of TinyML models to the managed devices, both the process of model training with Edge Impulse and manage the deployment with P15.

## Topics

- Connect Edge Impulse Project
- Plug and Play model
- Update ML model/Firmware with BLE connect app

# Azure deploy

Project 15 is quickly set up in Microsoft Azure by the provided ARM template. To demonstrate how it can be adjusted to the case of adding Edge Impulse models and in particlar the use case of SmartParks and their Elephant Collar, the following changes will direct to the demo code:
- url and branch in `PrivateModelRepo`
- url for *webApp* and *functions* in `git-repo`

## 1. Open ARM Template Deployment

Click **Deploy to Azure** button below  

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSaraOlsson%2Fproject15%2Fmaster%2FEdge-Impulse-Guide%2Fazuredeploy.json" target="_blank"><img src="deploy-to-azure.svg"/></a>

> [!TIP]  
> Right click the button below and select **Open link in new tab** or **Open lin in new window**

# Added to P15
- Module in Web Portal for Edge Impulse connection and actions (UI + backend)
    - Sample project in Edge Impulse made public
- File upload to P15 IoT Hub (via Azure Function)
- (Functionallity to save telemetry to Storage Account and forward it to Edge Impulse) 

# File upload (training data upload)
- Enable File Upload in IoT Hub by connecting a Storage Account to it. 
- Use added function in `project15-openplatform-functions` HTTP endpoint

    - Ingest from Azure Blob Storage
    - Ingest from http POST request

This endpoint makes a POST request to `http://ingestion.edgeimpulse.com/api/training/data`

# Get Edge Impulse model 

(Download model from the Portal or backend)

## Edge Impulse API

In the [Edge Impulse API](https://docs.edgeimpulse.com/reference#edge-impulse-api), we can use the [download endpoint](https://docs.edgeimpulse.com/reference#downloadbuild), where the *type* parameter implies which microcontroller the firmware is built for, or what library the model is packaged as. 

`https://studio.edgeimpulse.com/v1/api/{projectId}`

- Get your project id from Edge Impulse studio.
- Look up what *type* you need, for example: 
    - *nordic-nrf52840-dk*  
    - *zip* for C++ library  
    - *openmv* for OpenMV library 
    - *runner-linux-aarch64* for embedded Linux  

# Connect Edge Impulse Project

Training of TinyML model takes place in the Edge Impulse studio. Added to P15-EI is a widget in the web portal to connect a Edge Impulse project by entering the project id. 

Choosing a model project will enable to 
- view model type and classes
- build and prepare firmware for update of IoT device

TODO: add this widget

# Plug and Play model

A PnP model describes what telemetry is expected and what actions can be made from cloud to device. An example of how the Elephant Edge collar device is easily managed with a PnP model is described.

OpenCollarElephant model which is found at the [iot-plugandplay-models](https://github.com/SaraOlsson/iot-plugandplay-models/blob/main/dtmi/nordicsemi/OpenCollarElephant.json) repository

# Update ML model/Firmware with BLE connect app



# Usage with Lora messages

Alternatives:
- Azure IoT Hub integration at The Things Network
- Use IoT Bridge by Azure (forward Lora messages with HTTP via Azure Function to IoT Hub) 

# 