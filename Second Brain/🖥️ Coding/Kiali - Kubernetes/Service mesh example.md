Sure, here is a simple diagram that shows the structure of a service mesh:

                           +-------------------+
                           |   Application 1   |
                           +-------------------+
                              |       |       |
                              |       |       |
                              v       v       v
                           +-------------------+
                           |       Sidecar      |
                           +-------------------+
                              |       |       |
                              |       |       |
                              v       v       v
                           +-------------------+
                           |   Application 2   |
                           +-------------------+
                              |       |       |
                              |       |       |
                              v       v       v
                           +-------------------+
                           |       Sidecar      |
                           +-------------------+
                        
In this diagram, the service mesh is shown as a network of [[sidecars]] that are deployed alongside the individual microservices in the application. The sidecars intercept and manage the communication between the microservices, providing the features and capabilities of the service mesh.

The applications themselves are shown as boxes in the diagram, and are connected to the sidecars through lines that represent the communication between them. The sidecars are shown as smaller boxes, and are responsible for routing the communication between the applications, and providing the features of the service mesh.

Overall, this diagram shows the basic structure of a service mesh, and how the sidecars provide the infrastructure for communication and coordination between the microservices in a distributed application.