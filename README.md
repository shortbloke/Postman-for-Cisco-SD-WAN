# Postman for Cisco SD-WAN 19.x

This public repo contains a [POSTMAN](https://getpostman.com) [environment](Cisco-SD-WAN-Environment.postman_environment.json) and [collection](Cisco-SD-WAN.postman_collection.json) that can be used to interact with the `Cisco SD-WAN 19.2 vManage REST API`. The environment is pre-configured to access the [Cisco DevNet: Cisco SD-WAN 19.2 Always On Sandbox for SD-WAN](https://sandbox-sdwan-1.cisco.com) fabric. You can edit the variables in the environment to point to your own vManage instance.

## API Calls in this Collection

This collection only includes calls to read (GET) information from the environment. It does not write changes to the vManage environment. The collection provides the following REST API calls to:

- Authenticate
  - Credentials provided in the [environment](Cisco-SD-WAN-Environment.postman_environment.json) are for the Always On environment.
  - Obtain X-XSRF-TOKEN to protect against [Cross-Site Request Forgery](https://www.cisco.com/c/en/us/td/docs/routers/sdwan/configuration/sdwan-xe-gs-book/cisco-sd-wan-API-cross-site-request-forgery-prevention.html)
    - Required for SD-WAN 19.2 and later. The collection automatically stores the token for later calls.
- List devices that are part of the SD-WAN fabric and show device status, counters, and interface statistics for all the interfaces in the fabric.
- List device templates
- List device policy
- Bulk API requests:
  - State [Bulk State API Documentation](https://sdwan-docs.cisco.com/Product_Documentation/Command_Reference/Command_Reference/vManage_REST_APIs/Bulk_APIs/Overview_of_Bulk_API_Operations)
    - Includes an undocumented endpoint (`/dataservice/data/device/state/CEdgeInterface`) for obtaining a list of all interfaces on Cisco IOS XE Routers including i.e. Cisco ISR and also cloud hosted CSR devices.
  - Statistics [Bulk Statistics API Documentation](https://sdwan-docs.cisco.com/Product_Documentation/Command_Reference/Command_Reference/vManage_REST_APIs/Bulk_APIs/Statistics)
    - _Data lags real-time by ~20mins_
- Real-Time monitoring [Real-Time Monitoring API Docuumentation](https://sdwan-docs.cisco.com/Product_Documentation/Command_Reference/Command_Reference/vManage_REST_APIs/Real-Time_Monitoring_APIs)

Feel free to modify them as you see fit and to add more calls to the collection.

## Requirements

The Postman collection and environment will need:

- Postman 6.4.4+
- Cisco SD-WAN powered by Viptela vManage 19.x or later
- If using version 18.x, the API uses port `8443` instead of the standard port `443`. This collection _should_ work with an 18.x environment if the environment variable `port` is set.

## Setup

If you don't have Postman already installed, you can download it from [here](https://getpostman.com). Once you install it, you can follow the steps below to import the collection and environment:

![Postman Image](./postman.png)

1. Click on `Import`, browse to the location where you cloned this repo and add the two files:
    1. `Cisco-SD-WAN-Environment.postman_environment.json`
    2. `Cisco-SD-WAN.postman_collection.json`
2. Make sure you select the `Cisco-SD-WAN-Environment` environment
3. Expand the collection and start making REST API calls.

You can also export the API call into your preferred programming language, like Python or Go.

![codesnip](./code_snip.png)

## Using self-signed certificate

In case your instance of vManage has a self signed certificate, you can disable `SSL certificate verification` in Postman's settings (File -> Settings -> General -> SSL certificate verification).
