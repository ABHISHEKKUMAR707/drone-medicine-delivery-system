# Drones Delivery Project

The Drone Delivery System for Medical Supplies to Remote and War-Hit Regions is a groundbreaking initiative designed to provide swift and efficient distribution of crucial medical supplies to areas that face logistical challenges due to remoteness or conflict. This innovative system utilizes advanced drone technology to overcome geographical barriers and deliver life-saving supplies to communities in need.

At its core, the system consists of a network of automated drones equipped with specialized compartments capable of carrying various medical supplies such as vaccines, medications, blood samples, and emergency equipment. These drones are designed to withstand diverse weather conditions and navigate challenging terrain with precision and reliability.

The operation of the drone delivery system begins with careful planning and coordination between healthcare providers, humanitarian organizations, and local authorities. Medical supplies are carefully packaged and loaded onto the drones at designated distribution centers or hubs strategically located near the affected regions.

Once airborne, the drones are guided by a combination of GPS technology and autonomous flight algorithms, ensuring accurate navigation to the intended destinations. Real-time monitoring and control systems allow operators to track the drones' progress and make necessary adjustments to their flight paths as needed.

Upon reaching their destination, the drones execute precise landing maneuvers, delivering the medical supplies directly to healthcare facilities, field hospitals, or designated drop-off points. This direct delivery approach eliminates the need for ground transportation, reducing delivery times and ensuring timely access to critical supplies.

The Drone Delivery System for Medical Supplies to Remote and War-Hit Regions offers several advantages over traditional delivery methods. It significantly reduces the time and cost associated with transporting supplies over long distances, bypasses roadblocks and other logistical obstacles, and minimizes the risk to delivery personnel operating in hostile environments.

Moreover, the system enhances the resilience of healthcare infrastructure in remote and conflict-affected areas, ensuring that essential medical services remain accessible even in the face of adversity. By leveraging cutting-edge technology and innovative solutions, this initiative represents a significant step forward in improving healthcare delivery and saving lives in some of the world's most challenging environments.


## Queries
The queries are for testing the functionality and requirements of the project. 

### Drones
1. List all drones
    ```graphql
    query {
       getAllDrones {
         id
         serialNumber
         model
         weightLimit
         battery
         state
         flagDelete
         createdAt
         updatedAt
       }
    }
    ```
2. Get drone by ID
    ```graphql
    query {
       getDroneById(id: 1) {
          id
          serialNumber
          model
          weightLimit
          battery
          state
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
3. List drones by state
    ```graphql
    query {
       getDronesByState(state: "IDLE") {
          id
          serialNumber
          model
          weightLimit
          battery
          state
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
4. Create drone
    ```graphql
    mutation {
       createDrone(input: {
          serialNumber: "DRN001",
          model: "LightWeight",
          weightLimit: 300,
          battery: 80
       }) {
          id
          serialNumber
          model
          weightLimit
          battery
          state
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
5. Update drone
    ```graphql
    mutation {
       updateDrone(input: {
          id: 1,
          model: "LightWeight",
          weightLimit: 300,
          battery: 80
       }) {
          id
          serialNumber
          model
          weightLimit
          battery
          state
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
6. change state drone by ID
    ```graphql
    mutation {
       changeStateDrone(id: 1)
    }
    ```
7. Temporary delete drone by ID, change flagDelete to true, is like a fake delete
    ```graphql
    mutation {
       temporaryDeleteDrone(id: 1)
    }
    ```
9. Permanent delete drone by ID
    ```graphql
    mutation {
       permanentDeleteDrone(id: 1)
    }
    ```


### Medications
1. List all medications
    ```graphql
    query {
       getAllMedications {
          id
          name
          weight
          code
          image
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
2. Get medication by ID
    ```graphql
    query {
       getMedicationById(id: 1) {
          id
          name
          weight
          code
          image
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
3. Create medication
    ```graphql
    mutation {
       createMedication(input: {
          name: "Medication-A",
          weight: 10,
          code: "MED001"
       }) {
          id
          name
          weight
          code
          image
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
4. Update medication
    ```graphql
    mutation {
       updateMedication(input: {
          id: 3,
          name: "Medication-E",
          weight: 40,
          code: "MED003"
       }) {
          id
          name
          weight
          code
          image
          flagDelete
          createdAt
          updatedAt
       }
    }
    ```
5. Temporary delete medication by ID, change flagDelete to true, is like a fake delete
    ```graphql
    mutation {
       temporaryDeleteMedication(id: 1)
    }
    ```
6. Permanent delete medication by ID
    ```graphql
    mutation {
       permanentDeleteMedication(id: 1)
    }
    ```


### BatteryLogs
1. List all battery logs
    ```graphql
    query {
       getAllBatteryLogs {
          id
          drone {
             id
             serialNumber
          }
          batteryLevel
          createdAt
          updatedAt
       }
    }
    ```
2. Get battery logs for drone ID
    ```graphql
    query {
       getBatteryLogsForDrone(droneId: 1) {
          id
          drone {
             id
             serialNumber
          }
          batteryLevel
          createdAt
          updatedAt
       }
    }
    ```
3. Delete all battery logs for drone ID
    ```graphql
    mutation {
       deleteBatteryLogsForDrone(droneId: 1)
    }
    ```


### DronesMedications
1. List all medications loaded for drone ID
    ```graphql
    query {
       getMedicationsForDrone(droneId: 1) {
          id
          batteryUse
          deliveryStatus
          medication {
             id
             code
             name
             weight
          }
       }
    }
    ```
2. List all drones that have a loaded medicine
    ```graphql
    query {
       getDronesForMedication(medicationId: 1) {
          id
          batteryUse
          deliveryStatus
          drone {
             id
             model
             battery
             state
             weightLimit
          }
       }
    }
    ```
3. Charge medicines to the drone, remember that the state of the drone must be LOADING, must have a battery above 25 and must not exceed the weight limit of the drone.
    ```graphql
    mutation {
       loadMedicationsToDrone(droneId: 1, medications: [1, 2, 3]) {
          batteryUse
          deliveryStatus
          droneId
          medicationId
       }
    }
    ```


## Requirements
List of all requirements and validations:

### Functional requirements
1. The service must allow to register a drone with the following fields:
   - [ ] Serial number with a maximum of 100 characters.
   - [ ] Drone model, with options: LightWeight, MiddleWeight, CruiserWeight, HeavyWeight.
   - [ ] Drone weight limit with a maximum of 500 grams.
   - [ ] Battery capacity (battery capacity) in percent.
   - [ ] State of the drone, with options: IDLE, LOADING, LOADED, DELIVERING, DELIVERED, RETURNING. 
2. Charging a drone with medicines:
   - [ ] The service must allow loading a drone with medication, ensuring that the total weight of the medication does not exceed the drone's weight limit.
   - [ ] A drone should not be allowed to be loaded if its battery level is below 25% (LOADING status).
3. Check the medicines loaded on a drone:
   - [ ] The service should allow consulting the list of medicines loaded on a specific drone.
   - [ ] The list should include the name, weight and code of each medicine, as well as the image associated with its case.
4. Check the drones available for loading:
   - [ ] The service must allow consulting the list of drones available for loading, i.e. those that are in IDLE status.
5. Check the battery level of a drone:
   - [ ] The service must allow querying the battery level of a specific drone.

### Non-functional requirements

1. Data format: 
   - [ ] All communication with the service must be in JSON format.
2. Project configuration and execution:
   - [ ] The project must be buildable and executable without problems.
   - [ ] A README file must be provided with detailed instructions on how to build, run and test the project.
   - [ ] A database that can be run locally, such as an in-memory database or one that can be run via a container, must be used.
3. Initial data loading:
   - [ ]  All data required for the execution of the service, such as reference tables or test data, must be preloaded into the database.
4. Unit test:
   - [ ] Although optional, it is suggested to include unit tests using JUnit.
5. Periodic battery verification task:
   - [ ] A periodic task should be introduced that checks the battery levels of the drones and creates a historical or audit event log for this.
6. Charge and status monitoring:
   - [ ] The service should implement the necessary validations to ensure that drones are not overloaded with drugs and do not enter LOADING state if the battery is below 25%.
7. Change history:
   - [ ] It is suggested to show how changes have been made to the project through the commit history in the code repository.


## Technologies
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![GraphQL](https://img.shields.io/badge/-GraphQL-E10098?style=for-the-badge&logo=graphql&logoColor=white)
![Apollo-GraphQL](https://img.shields.io/badge/-ApolloGraphQL-311C87?style=for-the-badge&logo=apollo-graphql)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Mocha](https://img.shields.io/badge/-mocha-%238D6748?style=for-the-badge&logo=mocha&logoColor=white)


