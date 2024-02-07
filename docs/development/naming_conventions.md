# Salesforce Naming Conventions
Naming Conventions for Customization and Configuration in Salesforce is an important consideration when creating custom modifications and applications on the platform.

1. **Descriptive and Specific Names:** When naming custom objects, fields, or other components, choose descriptive and specific names. Avoid overly general terms like “ProductLine,” which may have different meanings depending on context.
2.	**Business Alignment:** Opt for names that align with our organization’s terminology. For example, use “IncomeSupportProgram” instead of generic terms to ensure consistency with business processes.

Remember, adhering to these naming conventions enhances readability and facilitates efficient management of our Salesforce environment.

## 1. Language
**Configurable metadata** (such as Custom Objects, Custom Fields, Process Builder, Flows, Apex, etc.) is created and named in the English language. This applies to both labels, API names, and help text. For metadata where labels are visible to the user, these must be translated to Norwegian using the **[Translation Workbench](https://help.salesforce.com/s/articleView?id=sf.workbench_overview.htm&type=5)**. There are two main reasons for this approach:

1. We want to adhere to English names at the **database and backend level**. This enhances the flow and readability of code, especially since English is already extensively used in standard functions and external libraries.
2. External interfaces will face requirements to support multiple languages. By introducing translation functionality via the Translation Workbench at an early stage, adaptations are ready to be translated into multiple languages as needed.

Remember that maintaining consistent naming conventions across different languages is crucial for clarity and maintainability in software development.

## 2. Casing Styles
When it comes to naming conventions, various casing styles exist. Let's explore the differences between them:

### Snake Case
- In snake case, words are separated by underscores (```_```).
- All letters are in lowercase.
- **Examples:**
    - `number_of_users = 34`
    - `hello_phrase = "Hello World"`

#### Screaming Snake Case
- This variant of snake case uses all uppercase letters.
- Also known as the "screaming snake case."
- **Examples:**
    - `NUMBER_OF_USERS = 34`
    - `HELLO_PHRASE = "Hello World"`

### Kebab Case
- Similar to snake case, but words are separated by dashes (```-```).
- All words are lowercase.
- Kebab case is a human-readable way to combine multiple words into a single identifier.
- **Examples:**
    - `number-of-users = 34`
    - `hello-phrase = "Hello World"`

### Camel Case
- In camel case, the first word starts with a lowercase letter.
- Each subsequent word begins with an uppercase letter.
- **Examples:**
    - `numberOfUsers = 34`
    - `helloPhrase = "Hello World"`

### Pascal Case
- Similar to camel case, but the first letter of the first word is also capitalized.
- Every word starts with an uppercase letter.
- **Examples:**
    - `NumberOfUsers = 34`
    - `HelloPhrase = "Hello World"`

Choose the appropriate casing style based on your programming language and coding conventions! 🚀

## 3. Custom Objects
### Rules for Naming
- **Object Label:** Singular, Pascal Case
- **Object Plural Label:** Plural, Pascal Case
- **Object Name (API Name):** Singular, Pascal Case (without underscores beyond the mandatory “__c”)

When naming custom objects within Salesforce, adhere to the following rules to ensure clarity and consistency:

1. **Uniqueness:** Custom object names must be **unique** across your organization. Begin each name with an **uppercase letter**.

2. **Descriptive and Whole Words:** Use **descriptive** and **whole words** for object names. Avoid excessive use of acronyms and abbreviations.

3. **Singular Form:** Choose **singular** names (e.g., "Review" instead of "Reviews," or "OrderItem" instead of "Order Items").

4. **No Underscores:** Avoid including underscores ("_") in object names.

5. **Consistent Object Label:** Whenever possible, align the **object label** with the object name. Consistency between the label and name ensures ease of navigation within Salesforce and finding the object in the various setup UIs.

6. **English Language Naming:** All naming conventions should be in **English**.

7. **Norwegian Translation:** When translating labels and user-facing text to Norwegian, **adhere to our organization’s specific terminology**. (***Tip:** Utilize Salesforce’s Translation Workbench for translating labels and user-facing text to Norwegian.*)

Remember, well-defined naming conventions contribute to a streamlined and efficient Salesforce configuration.

### Prefixing
As a general rule, avoid adding team names, application acronyms to object names. Instead use the description field to add team or application ownership to the object. (*Another and better solution will be made for handling this later.*)

### Exceptions
When naming custom objects within Salesforce, consider the following exceptions to enhance clarity and maintain consistency:

1. **Acronyms and Abbreviations:** Widely used and commonly understood acronyms and abbreviations can replace the long form. For instance, "HTTP," "URL," or "NAV" are acceptable.

2. **Underscores for Application Prefix:** Adding an underscore is acceptable when prefixing the object name to denote its association with an application. For example:
   - Correct: **OrderApplication_Order**
   - Correct: **OrderApplication_OrderItem**
   - Note: **OrderItem** does not have any underscores.

Remember, adhering to these exceptions ensures a balance between readability and precision in your naming conventions.

### Demonstrative Example
The following are examples of custom object naming that should *not* be used 

|Object Name (API) | Reason |
|-------------|:--------|
```CustAsset```| Abbreviations have made this object name hard to understand 
```Orders``` | Object names should always be singular. 
```Order_Item``` | Object names should not have underscores. 

The following are examples of the naming convention that will be used:

|Object Name (API) | Reason |
|-------------|:--------|
```CustomerAsset``` | Removing ambiguity from the name will improve readability and maintainability 
```Order``` |  Making object names singular will ensure a standard naming convention across all objects. 
```OrderItem``` | Removing all underscores will help keep a standard naming convention as many times there are words that some may separate into two words and other may not. For example: ```Zipcode``` vs. ```Zip Code```.

The following are examples shows valid naming conventions for Object Label, Object Plural Label and Object Name (API):

| Object Label | Object Plural Label | Object Name (API) |
|:-------------|:-------------|:-------------|
Shipping Invoice | Shipping Invoices | ```ShippingInvoice__c```
Inclusion Opportunity | Inclusion Opportunities | ```InclusionOpportunity__c```

____

