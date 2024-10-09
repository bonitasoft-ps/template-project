# Good Practices]

## Introductio
This page has been created to make it easier to know, list, and maintain good practices in order to advise our clients on good practice audits.

## Best Practices Sections

- [1. Security](#1-security)
- [2. BPM (Business Process Management)](#2-bpm-business-process-management)
- [3. Connectors](#3-connectors)
- [4. UI Designer](#4-ui-designer)
- [5. Rest APIs Extension](#5-rest-apis-extension)
- [6. BDM (Business Data Model)](#6-bdm-business-data-model)
- [7. General](#7-general)

### 1. Security
> Security practices help protect sensitive data and ensure system integrity. This includes enforcing strong authentication mechanisms, encryption of data at rest and in transit, and regular security audits.


### 2. BPM (Business Process Management)
> Best practices in BPM involve optimizing workflows, ensuring process scalability, and maintaining clarity in process documentation.

| #  | Best Practice                                                                                                                                                          |
|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1  | Leave the heaviest tasks to connectors, leaving operations for simpler functionalities (assignments, etc.).                                                          |
| 2  | Avoid infinite multi-instances.                                                                                                                                     |
| 3  | Avoid infinite cyclic flows:                                                                                                                                       | 
|    | - Always a condition for termination.                                                                                                                                  |
|    | - Even a "manual" option for termination.                                                                                                                            |
| 4  | Reuse code by implementing or using custom connectors.                                                                                                               |
| 5  | Task error management:                                                                                                                                               |
|    | - Capturing possible errors.                                                                                                                                          |
|    | - Terminating, warning, retrying, etc.                                                                                                                                 |
| 6  | Define and analyze the use of external libraries.                                                                                                                    |
| 7  | Check if all methods are used in all processes:                                                                                                                     |
|    | - Analyze whether it is feasible to separate the libraries so that each process has its dependencies.                                                                  |
|    | - Avoid including the same library in all processes.                                                                                                                  |
| 8  | Verify that it is not possible to make sub-processes to facilitate the injection of the libraries to a single process or processes.                                    |
| 9  | Last option: inject the library into the application server (../lib).                                                                                               |
| 10 | Try to develop the processes in three levels:                                                                                                                       |
|    | - Level 1: Processes with the main logic or with the stages of the business process.                                                                                   |
|    | - Level 2: Sub-processes with business logic for each stage.                                                                                                          |
|    | - Level 3: Sub-processes with the technical section of the functionalities.                                                                                           |
|    | - Changes in sub-processes should not impact instances of the main processes.                                                                                         |
| 11 | Within the 3-level methodology:                                                                                                                                     |
|    | - If the process requires auditing, that operation will be carried out at level 2, even if it is a technical operation.                                               |
| 12 | Define a contract for information sent to the thread:                                                                                                               |
|    | - Whenever implementing a thread that is called from a calling activity.                                                                                              |
|    | - Helps clarify what information is sent.                                                                                                                            |
| 13 | While using variables, there may be extra variables in the thread that do not need to be sent during instantiation.                                                   |
| 14 | With the contract:                                                                                                                                                   |
|    | - Define the precise information to send to the thread.                                                                                                               |
|    | - Initialise variables with contract information if necessary.                                                                                                        |
| 15 | Follow a special nomenclature for contract information:                                                                                                              |
|    | - Example:                                                                                                                                                            |
|    |   - Contract: `codigoC`, `codigo_c`,...                                                                                                                                |
|    |   - Variables: `codigo`, `codigoV`, `codigo_v`,...                                                                                                                   |
| 16 | Manage necessary operations in applications:                                                                                                                          |
|    | - For integrations with other systems.                                                                                                                                |
|    | - Actions (insert, update, delete) on BDM, other databases, etc.                                                                                                     |
| 17 | Use a .bar file for each environment:                                                                                                                                |
|    | - Define parameters, actors, etc. according to the selected environment.                                                                                             |
| 18 | Ensure all configurations (actors, and parameters) per environment are filled in.                                                                                   |
| 19 | Define BPM elements with meaningful names:                                                                                                                           |
|    | - Avoid using names like Gate1, Start1, End1, Step1, etc.                                                                                                           |
| 20 | Care must be taken to define messages that are not captured:                                                                                                        |
|    | - They will be listened to infinitely, causing the database to grow.                                                                                                 |
| 21 | Possible solutions:                                                                                                                                                  |
|    | 1. Capture the message (through events that capture messages).                                                                                                      |
|    | 2. Capture the message in a generic way (event sub-process).                                                                                                        |
|    | 3. Check before sending the message to verify the instance is active.                                                                                               |
| 22 | Review how actors are obtained, how actor filters are implemented.                                                                                                   |


## Versión en Español

### Introducción
Esta página se ha creado para facilitar el conocimiento, la enumeración y el mantenimiento de buenas prácticas con el fin de asesorar a nuestros clientes en auditorías de buenas prácticas.

### Secciones de Buenas Prácticas

-


### 3. Connectors
Connectors should be reusable, modular, and follow standardized error handling patterns to ensure system stability and flexibility.

### 4. UI Designer
The UI should be user-friendly, accessible, and consistent with design guidelines to improve the user experience and accessibility.

### 5. Rest APIs Extension
Ensure APIs are versioned, secure, and well-documented. Best practices include using proper HTTP methods, status codes, and request validation.

### 6. BDM (Business Data Model)
Maintain a clear and scalable data model with proper relationships, data integrity, and documentation for ease of use and future expansion.

### 7. General
General best practices include writing maintainable code, following coding standards, and ensuring proper testing and code review processes.

