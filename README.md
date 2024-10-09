# [Good Practices](#english-version)

## Introduction
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
Security practices help protect sensitive data and ensure system integrity. This includes enforcing strong authentication mechanisms, encryption of data at rest and in transit, and regular security audits.
Avoid infinite multi-instances.

Avoid infinite cyclic flows (always a condition for termination, and even a "manual" option for termination).

Reuse code by implementing or using custom connectors.

Task error management by capturing possible errors and terminating, warning, retrying, etc.

Define and analyze the use of external libraries.

Check if all methods are used in all processes. In other words, analyze whether it is feasible to separate the libraries so that each process has its dependencies and the same library does not have to be included in all processes.

Verify that it is not possible to make sub-processes to facilitate the injection of the libraries to a single process or processes.

Last option: inject the library into the application server (../lib).

Try to develop the processes in three levels.

Level 1: Processes with the main logic or with the stages of the business process.

Level 2: Sub-processes with business logic for each stage.

Level 3: Sub-processes with the technical section of the functionalities.

It allows that if there are changes uploading the changes to the sub-processes, it does not impact on the instances of the main processes.

Within the 3-level methodology, if the process requires auditing, that operation will be carried out at level 2, even if it is a technical operation.

Whenever you implement a thread that is called from a calling activity, define a contract to define the information that is sent to the thread.

Although this can be done with variables, there may be more variables in the thread that do not need to be sent during instantiation.

With the contract, you define the precise information you want to send to the thread, and then if necessary initialise the variables with the information in the contract.

It may be interesting to follow a special nomenclature to define the contract information so that you know whether it is variable or contract information.

For example:

- Contract: codigoC, codigo_c,...
- Variables: codigo, codigoV, codigo_v,...

Manage all the necessary operations in the applications for integrations with other systems, or actions (insert, update, delete) on BDM, other databases, etc.

Use a .bar file for each environment, defining in the Studio the parameters, actors, etc. according to the selected environment.

Ensure that all configurations (actors, and parameters) per environment are filled in.

Define the names of the BPM elements with meaningful names. Do not use e.g. Gate1, Start1, End1, Step1, etc.

Care must be taken to define messages that are not captured. Since they will be listened to infinitely. It will cause the database to grow.

Possible solutions:

- Capture the message (through events that capture messages).
- Capture the message in a generic way (event sub-process).
- Perform a check prior to sending the message to verify that the instance or instances of the process or processes to which they are sent are active, and have not finished, and even if the flow has already passed through where the event can be captured.

Review how actors are obtained, how actor filters are implemented.


### 2. BPM (Business Process Management)
Best practices in BPM involve optimizing workflows, ensuring process scalability, and maintaining clarity in process documentation.
- **Leave the heaviest tasks to connectors:**  
> **Tip:** Assign complex tasks to connectors while reserving simpler functionalities (like assignments) for operations.

- **Avoid infinite multi-instances:**  
> **Reminder:** Implement checks to prevent infinite multi-instance scenarios in your processes.

- **Avoid infinite cyclic flows:**  
> **Advice:** Always include a condition for termination in cyclic flows, and consider a "manual" option for stopping them if necessary.

- **Reuse code by implementing or using custom connectors:**  
> **Best Practice:** Strive to implement or utilize custom connectors to avoid code duplication and enhance maintainability.

- **Task error management:**  
> **Caution:** Capture potential errors in tasks and handle them by terminating, warning, retrying, etc.

- **Define and analyze the use of external libraries:**  
> **Important Note:**  
  - Verify that all methods are utilized in all processes to determine if libraries can be separated for better dependency management.
  - Check if it's feasible to create sub-processes for library injection into specific processes.
  - As a last resort, consider injecting libraries into the application server (../lib).

- **Try to develop processes in three levels:**  
> **Strategy:**  
  - **Level 1:** Main processes containing core logic or business process stages.
  - **Level 2:** Sub-processes focused on business logic for each stage.
  - **Level 3:** Sub-processes managing the technical aspects of functionalities.
  
  This structure allows for changes in sub-processes without affecting ongoing instances of main processes.

- **Within the 3-level methodology:**  
> **Note:** If a process requires auditing, conduct that operation at level 2, even if it's a technical task.

- **Whenever you implement a thread from a calling activity:**  
> **Suggestion:** Define a contract for the information sent to the thread.  
  - Although variables can be used, ensure the contract specifies what information is required for initialization.
  - Following a special naming convention helps differentiate between variable names and contract information.
  
  For example:
  - Contract: `codigoC`, `codigo_c`,...
  - Variables: `codigo`, `codigoV`, `codigo_v`,...

- **Manage necessary operations for integrations:**  
> **Reminder:** Ensure all required actions (insert, update, delete) on BDM and other databases are properly managed within applications.

- **Use a .bar file for each environment:**  
> **Best Practice:** Define parameters, actors, etc., in the Studio according to the selected environment.

- **Ensure all configurations per environment are filled in:**  
> **Caution:** Double-check that configurations for actors and parameters are complete for each environment.

- **Define BPM element names meaningfully:**  
> **Advice:** Use descriptive names for BPM elements instead of generic labels like Gate1, Start1, End1, Step1, etc.

- **Care must be taken with uncaptured messages:**  
> **Warning:** Care must be taken to define messages that are not captured. Since they will be listened to infinitely. It will cause the database to grow. 
> **Possible Solutions:**
> 1. Capture the message through events that capture messages.
> 2. Capture the message generically via an event sub-process.
> 3. Perform a pre-check before sending the message to ensure that the instances of the target processes are active and have not finished processing.

- **Review how actors are obtained:**  
> **Best Practice:** Evaluate the methods used to obtain actors and how actor filters are implemented to ensure efficiency and clarity in your processes.

---

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

