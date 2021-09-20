# docker-compose-experiment
Simple project to reproduce the problem with Avast Docker-Compose Gradle plugin problem

This project does nothing but provide a Gradle build file, `build.gradle` which adds the plugin `com.avast.gradle.docker-compose` with version `0.14.9`.

Running the command `gradle composeUp` will result in the pull of the official MongoDB image as per the `docker-compose.yml` specification. The output is:
```
mongodb_container Pulled
Network 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__default  Creating
Network 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__default  Created
Volume "50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__mongodb_data_container"  Creating
Volume "50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__mongodb_data_container"  Created
Container mongodb  Creating
Container mongodb  Created
Container mongodb  Starting
Container mongodb  Started
no such service: mongodb_container
Container mongodb  Stopping
Container mongodb  Stopped
Container mongodb  Stopping
Container mongodb  Stopping
Container mongodb  Stopped
Container mongodb  Removing
Container mongodb  Removed
Volume 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__mongodb_data_container  Removing
Network 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__default  Removing
Volume 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__mongodb_data_container  Removed
Network 50661f3337ac19f26efcadeddb32f67d_dockercomposeexperiment__default  Removed
```

When running the equivalent docker-compose command (`docker-compose up -d`), the container is successfully started and running.

```
PS D:\Projects\temp\docker-compose-experiment> docker-compose up -d
[+] Running 11/11
 - mongodb_container Pulled                                                                                                                                                                                                          28.1s
   - 35807b77a593 Pull complete                                                                                                                                                                                                       6.0s
   - 664b0ebdcc07 Pull complete                                                                                                                                                                                                       6.2s
   - d598f4d3c081 Pull complete                                                                                                                                                                                                       6.6s
   - 291455135b00 Pull complete                                                                                                                                                                                                       7.3s
   - b46409342f13 Pull complete                                                                                                                                                                                                       7.5s
   - ff2b9c6e6f3a Pull complete                                                                                                                                                                                                       7.6s
   - 149f6335fc27 Pull complete                                                                                                                                                                                                       7.8s
   - baeb6f3bec76 Pull complete                                                                                                                                                                                                      24.3s
   - 8617caab2de5 Pull complete                                                                                                                                                                                                      24.4s
   - 067d70de7828 Pull complete                                                                                                                                                                                                      24.4s
[+] Running 3/3
 - Network docker-compose-experiment_default                  Created                                                                                                                                                                 0.7s
 - Volume "docker-compose-experiment_mongodb_data_container"  Created                                                                                                                                                                 0.0s
 - Container mongodb   

PS D:\Projects\temp\docker-compose-experiment> docker-compose ps
NAME                COMMAND                  SERVICE             STATUS              PORTS
mongodb             "docker-entrypoint.s…"   mongodb_container   running             0.0.0.0:27017->27017/tcp, :::27017->27017/tcp
PS D:\Projects\temp\docker-compose-experiment>
```
