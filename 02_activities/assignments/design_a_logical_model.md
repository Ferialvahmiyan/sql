# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

![image](https://github.com/user-attachments/assets/0d8cd163-d659-4d46-b28b-328d5793bb17)


## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

![image](https://github.com/user-attachments/assets/b75466bb-daa5-4145-8fee-4ff72d804575)


## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._

Bonus: Are there privacy implications to this, why or why not?
```
Customer_Address Table (Overwriting Changes)
Column Name		   Data Type		Description
CustomerID	      INT (FK)	      References the customer
AddressLine1	   VARCHAR	      Current street address
AddressLine2	   VARCHAR	      Additional address info (if any)
City	            VARCHAR	      Current city
State	            VARCHAR	      Current state
PostalCode	      VARCHAR	      Current postal code
Country	         VARCHAR	      Current country
LastUpdatedDate   DATE	          Date when the address was last updated

•	Characteristics:
o	This table holds one record per customer.
o	The address is overwritten each time a change occurs, without keeping a history of previous addresses.
Type: This is Type 1 Slowly Changing Dimension (SCD), where the new data overwrites the existing data without retaining historical information.

Customer_Address Table (Retaining Changes)
Column Name		Data Type		   Description
AddressID	    INT (PK)	      Unique identifier for the address
CustomerID	    INT (FK)	      References the customer
AddressLine1	 VARCHAR	         Street address
AddressLine2	 VARCHAR	         Additional address info (if any)
City	          VARCHAR	         City
State	          VARCHAR	         State
PostalCode	    VARCHAR	         Postal code
Country	       VARCHAR	         Country
StartDate	    DATE	            Date when this address became valid
EndDate	       DATE(nullable)   Date when this address was replaced
IsCurrent	    BOOLEAN	         Indicates whether this is the current address

•	Characteristics:
o	Multiple records per customer. A new row is created for each address change.
o	The EndDate column tracks when an address is no longer valid, while the IsCurrent column helps identify the most recent address.
Type: This is Type 2 Slowly Changing Dimension (SCD), where new data is added as a new row, and historical data is preserved.

Bonus: Yes, there are potential privacy implications:

Type 1 (Overwriting):
Lower risk: Since only the current address is stored, sensitive information from past addresses is not retained.
Privacy issue: Overwriting might miss important audit trails or historical data, which could be required for legal or compliance purposes.
Type 2 (Retaining History):
Higher risk: Retaining historical addresses may pose privacy concerns, especially if customers are unaware that old addresses are stored indefinitely.
Data retention concerns: Regulations may require companies to limit the retention of customer data, particularly sensitive personal information like addresses.
Security risks: If historical address data is not properly protected, it could expose personal information in the event of a data breach.
```

## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?
```
1- It has different column for indicating PK, FK and ...
2- It seperated each table into two part. One for PK and FK fields and the other is for all other fields inside the table.

I won't change my design as I think this make the table so complicated and it cannot be easily understood.
```

# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `September 28, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-4-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
