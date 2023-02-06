# RPS_Container_Apps
Deployment and infrastructure for RPS on ACA

## Gateway alternatives
- Api Gateway (service)
- Api (self hosted in ACA)
- Custom - YARP

## Local

**Step 1** - Run the gateway localy. 
> Port 5003 is specified in the launchSettings.json
```
dapr run --app-id rps-gateway --app-port 5003 --dapr-http-port 3500 -- dotnet run
```

**Step 2** - Run RPS container with a dapr side-car.

```
dapr run --app-id rps-game --app-port 80 -- docker run -p 80:80 ghcr.io/perokvist/fiffi/rps.web:latest 
```

> Note that we don't set any port for rps-game to communicate with the side-car yet.

**Step 3** - Verify
Running http://localhost:5003/games should now go through the proxy, with DAPR service location, to the RPS game service.

https://docs.dapr.io/developing-applications/sdks/dotnet/dotnet-development/dotnet-development-dapr-cli/

https://github.com/marketplace/actions/azure-container-apps-build-and-deploy



