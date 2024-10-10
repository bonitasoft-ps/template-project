# Good Practices

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
> Security practices help protect sensitive data and ensure system integrity. This includes enforcing strong authentication mechanisms, encryption of data at rest and in transit, and regular security audits.


### 2. BPM (Business Process Management)
> Best practices in BPM involve optimizing workflows, ensuring process scalability, and maintaining clarity in process documentation.

1. Leave the heaviest tasks to connectors, leaving operations for simpler functionalities (assignments, etc.).
2. Avoid infinite multi-instances.
3. Avoid infinite cyclic flows (always a condition for termination, and even a "manual" option for termination).
4. Reuse code by implementing or using custom connectors.
5. Task error management by capturing possible errors and terminating, warning, retrying, etc.
6. Define and analyze the use of external libraries.
- Check if all methods are used in all processes. In other words, analyze whether it is feasible to separate the libraries so that each process has its dependencies and the same library does not have to be included in all processes.
- Verify that it is not possible to make sub-processes to facilitate the injection of the libraries to a single process or processes.
   Last option: inject the library into the application server (../lib).
7. Try to develop the processes in three levels.
- Level 1: Processes with the main logic or with the stages of the business process.
- Level 2: Sub-processes with business logic for each stage.
- Level 3: Sub-processes with the technical section of the functionalities.
   It allows that if there are changes uploading the changes to the sub-processes, it does not impact on the instances of the main processes.
8. Within the 3-level methodology, if the process requires auditing, that operation will be carried out at level 2, even if it is a technical operation.
9. Whenever you implement a thread that is called from a calling activity, define a contract to define the information that is sent to the thread.
- Although this can be done with variables, there may be more variables in the thread that do not need to be sent during instantiation.
- With the contract, you define the precise information you want to send to the thread, and then if necessary initialise the variables with the information in the contract.
- It may be interesting to follow a special nomenclature to define the contract information so that you know whether it is variable or contract information.
- For example: 
    - Contract: `inputCode`, `codeC`, `codeInput`,...
    - Process Variables: `varCode`, `codeV`, `codeVar`,...
10. It is very interesting to name the variables according to their type in order to differentiate them and avoid problems by naming them in the same way. Sometimes Bonita Studio itself prevents you from naming them with the same name, but this way you can identify everything quickly.
- For example: 
    - Contract: `inputCode`, `codeC`, `codeInput`,...
    - Process Variables: `varCode`, `codeV`, `codeVar`,...
    - Task Variables: `taskVarCode`, `codeT`, `codeTaskVar`,...
    - Parameters: `paramCode`, `codeP`, `codeParam`,...
    - BDM Variables:  `bdmObject`, `objectB`, `objectBdm`, `object`,...
    - Script Variables: `auxCode`, `codeAux`, `code`,...
10. Manage all the necessary operations in the applications for integrations with other systems, or actions (insert, update, delete) on BDM, other databases, etc.
11. Use a .bar file for each environment, defining in the Studio the parameters, actors, etc. according to the selected environment.
12. Ensure that all configurations (actors, and parameters) per environment are filled in.
13. Define the names of the BPM elements with meaningful names. Do not use e.g. Gate1, Start1, End1, Step1, etc.
14. Care must be taken to define messages that are not captured. Since they will be listened to infinitely. It will cause the database to grow.
    Possible solutions:
    1. Capture the message (through events that capture messages).
    2. Capture the message in a generic way (event sub-process).
    3. Perform a check prior to sending the message to verify that the instance or instances of the process or processes to which they are sent are active, and have not finished, and even if the flow has already passed through where the event can be captured.
15. Review how actors are obtained, how actor filters are implemented.

### 3. Connectors
> Connectors should be reusable, modular, and follow standardized error handling patterns to ensure system stability and flexibility.

1. Error handling by capturing errors and displaying them in the log.
2. Making sure to close connections in finally.
3. Try not to return complex objects that depend on libraries (json object, "invoice", ... the library must be added in the connector and in the process); do not return BDM objects. Return externally readable objects, for example a Map object.
4. Do not have too many dependencies; try to encapsulate the logic.
5. Connectors that are developed outside the Studio with unit tests.
6. Catch errors; if it fails, you should know why it failed (try catch, logs, etc).
7. Use parameters via the expression editor to define the input data to the connector.

### 4. UI Designer
> The UI should be user-friendly, accessible, and consistent with design guidelines to improve the user experience and accessibility.

1. Define correct number of REST API Extensions, do not call more than once to the same service (by fragments or by widgets). Limiting the number of API calls.
2. Reuse code by implementing or using custom widgets.
3. Include in the constraints via Widget, via JS, and/or via contract.
4. External API to retrieve information at the top of the page, and you want to refresh information, use interpolation.
5. Define one or more controller classes (ctrl), all business logic.
6. Use js functions to process data, open modals, etc. (a kind of library).
7. Use widgets do not use angular js services (it is easier to migrate widgets using only javascript).
8. Widgets should not make rest calls, depending on whether the team is technical or not, but it is better to externalise the calls from outside, from the pages or forms.
   On a page or form in its page or form information section, the APIs that are used on that page or form are indicated. If calls are made from widgets, they never appear, and permissions must be managed manually.
   If fragments are used, calls should generally be made from fragments.
9. It is recommended to make widgets that are dumb and the fragments (for reuse) or, failing that, the page or form that implements the logic.
10. Define the look and feel using responsive functionality, different sizes, ...
11. Define different variables:
   - Java script variable called "log": show with the console.log variables or possible warnings or errors. Help for the developer
   - Url parameter called "debug": if true, a text area will be shown where variables are shown with the content, to help the development {{ variable | json }}.
   - Temp variable: with different nested variables
   - Java script variable called "functions": with the functions you want to use.
12. Use fragments to improve maintainability and reusability 

### 5. Rest APIs Extension
> Ensure APIs are versioned, secure, and well-documented. Best practices include using proper HTTP methods, status codes, and request validation.

1. It is recommended to use it to retrieve information for display.
2. Any action should be done through a process. If an action is taken, do it against Bonita, not to the outside world.
3. All expensive queries should be done from the Rest API Extension (server), instead of from the browser.
4. You have read access to the WDB; all other actions should be performed from the processes.
5. You can access other databases, but be sure to close connections.
6. You can access other REST APIs and other Web Services (WS), but only for reading or querying.
7. It is important to carry out a good management and definition of permissions and organisation.

### 6. BDM (Business Data Model)
> Maintain a clear and scalable data model with proper relationships, data integrity, and documentation for ease of use and future expansion.

1. What to do when a query is needed to obtain information from two or more BDM tables? Can queries be made with JPQL on several objects? No. It is recommended to develop a Rest API Extension that executes the query directly.
2. Specify unique elements.
3. Specify indexes according to the queries performed (predefined and custom queries do not create indexes automatically). It is important not to generate indexes just for the sake of generating them. Review the queries used and generate indexes only for the queries used.
4. Define the necessary queries with the necessary fields, no more.
5. Define accesses correctly.
6. Lazy instead of eager (Use Lazy whenever possible, except in cases of special needs).
7. Use a naming convention for BDM Objects (i.e. XXXObject, where XXX is the project trigram and object the name of the BDM object (the DB table).)
8. A modification of the BDM should never be made outside the process because it could not be used within the process.


### 7. General
> General best practices include writing maintainable code, following coding standards, and ensuring proper testing and code review processes.

1. Use descriptions to generate the project documentation
2. Use Bonita Test Toolkit to perform tests on processes.
3. Define unit tests on connectors, etc.
4. Define and use BCD for the automatic deployment of processes, facilitating deployment and avoiding errors.
5. Review dynamic and static permissions for profiles. Get all the permissions associated with the profiles. Get a list of the applications and their profiles, which profiles apply to each application. That is, which persons, groups or roles have access to the applications.
6. **CLEAN CODE**
- Clean Code refers to a programming style that emphasises readability, maintainability and clear structuring of source code. Robert C. Martin, also known as "Uncle Bob", wrote a book called "Clean Code: A Handbook of Agile Software Craftsmanship", where he presents principles and practices for writing clean, quality code.
- This style is proposed because project code at times has not been thought of and implemented as maintainable, readable and reusable.
- Here are some key Clean Code principles that can be applied to both Java and Groovy:
   1. **Meaningful Names:**
      - Use descriptive names for classes, methods, variables, and other code elements.
      - Avoid short, ambiguous names. A good variable or method name should explain its purpose without the need for additional comments.
   2. **Small Functions/Methods:**
      - Keep your functions/methods short and focused on a single responsibility.
      - If a function is long, consider breaking it into smaller functions.
   3. **Meaningful Comments:**
      - Use comments when necessary to explain the "why" behind certain decisions.
      - Focus on writing clear, self-explanatory code before resorting to comments.
   4. **Avoid Duplicity:**
      - Don't repeat code. Use functions/methods and classes to encapsulate and reuse logic.
      - Duplication of code makes maintenance difficult and increases the likelihood of errors.
   5. **Structure and Organisation:**
      - Maintain a consistent and organised code structure.
      - Group functions/methods and related variables into logical classes and packages.
   6. **Elegant Error Handling:**
      - Try to handle errors elegantly and provide meaningful error messages.
      - Avoid traps such as handling overly broad exceptions or ignoring errors.
   7. **Automated Testing:**
      - Write unit tests to validate the behaviour of your functions/methods.
      - Make sure your tests provide adequate coverage.
   8. **Consistent Alignment and Formatting**
      - Maintain consistent formatting throughout your code.
      - Use spaces or tabs consistently and align code so that it is easy to read.
   9. **Limit Function/Method Parameters:**
      - Avoid functions/methods with a large number of parameters. If you have too many parameters, you may need to re-evaluate your design.
   10. **Use Libraries and Frameworks:**
      - Take advantage of existing libraries and frameworks instead of reinventing the wheel.
      - If you use Groovy together with Java, familiarise yourself with the best practices of both languages. 
- **To carry out these principles in Java and Groovy:**
   - Conduct Code Reviews: Collaborate with your team to review code regularly. Discuss and adjust based on feedback.
   - Participate in the Community: Take advantage of online resources, forums, and communities to learn from others and share knowledge.
   - Automated Testing: Write unit and integration tests to validate your code.
   - Constantly Refactor: Watch for refactoring opportunities to continually improve code quality.
   - Apply SOLID Principles: Familiarise yourself with the SOLID principles of software design and try to apply them in your code.
- Remember that clean code is subjective in many ways and can vary depending on the context and preferences of the team.
- The key is communication and collaboration to establish standards and practices that everyone on the team understands and accepts.

