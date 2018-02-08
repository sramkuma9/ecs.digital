# ecs.digital
Automation test for ECS.

Read Me File for ECS- Digital Test Automation.

Test Scenarios:
1) Valid Submission :
	Automated, this test is covered in src/test/ECSRequirement.java  This test is automated 	as per the requirement from ECS.
2) Invalid Submission:
	This scenario covers both positive and negative scenarios and is partly automated (details 	below), this test is covered in 	src/test/ValidAndInvaidSubmission.java
  
		a) Automated Scenarios:
			1) Blank fields validation:
		   	 This covers name, email and message fields in the contact us page.
			2) Invalid email ID validation:
		     This covers invalid email formats.
			3) Test send button (email acknowledgement):
		     Checking the confirmation message displayed in the UI. The successful submission of details results in a database 					 entry and hence, the database entry or the email server is not automated.
			4) Validate maximum length of text fields:
		b) Not Automated Scenarios:   
			1) Test Call Us button
			2) Test Email Us button:
			3) All the text in the contact us page (for spelling and grammar)
4) Cross Browser Testing 
5) Mobile Testing

Instructions to build and run:
1) Link to the git repo - https://github.com/sramkuma9/ecs.digitalgit
2) Import the code into Eclipse (or similar IDE) and build and Run (Before executing check the platform limitations section on chrome driver details.)

Platform limitations:
None. However, the path for the chrome driver is provided in src/lib/BrowserFunctions.java 
This needs to be changed to point to the correct location in the machine where the test is executed.

Dependencies:
1) The below external Jar files need to be imported in Eclipse project.
2) Selenium WebDriver
3) Junit
4) Cucumber
5) JRE, JDK
6) Chrome driver (exe file) and chrome browser

Improvements:
1) Currently the test for checking the valid submission is done based on the alert message received after a failure to send the contact details (THERE WAS AN ERROR TRYING TO SEND YOUR MESSAGE. PLEASE TRY AGAIN LATER.) I believe this test should be based on the successful message in the UI. Since the Qaworks website was not able to send the details (maybe the email server is down), and failed with an error message, I used the failure message.
2) system.out.println is used in the code, this is because I am assuming the regression pack will be integrated with jenkins and will be executed as an over night build. When this happens, all an automated tester has to do is check the console messages in jenkins if a automatic mail is triggered for failure. If this setup with jenkins is not present, I can change these to log messages or something similar to fit in to the available framework within the organization.
3) assert function is not used in any of the tests because, the assert function will break the execution when there is a failure. Again if there is a requirement to use assert, I can modify the code.

Observations:
1) Validation Defect in 'Name' field: The 'Name' field currently accepts an all numeric value with no alphabet. It is recommended that there is a validation rule to check for at least 1 alphabet to be received for the 'Name' field or possibly raise an alert for any numerical value input.
2) Usability Defect in 'Response' message: When the 'Send' button is pressed after valid input for Name, Email and Message field, a response message is displayed as 'THERE WAS AN ERROR TRYING TO SEND YOUR MESSAGE. PLEASE TRY AGAIN LATER'. However, the font colour of the message blends with the background and hence is not readable unless it is highlighted. It is to be noted that the alert message is readable on other scenarios observed.
3) Potential Improvement: There is no captcha in the 'Contact Us' page and hence, there is a potential risk of an automated script spamming and overlaoding the server with requests bearing valid input values. This is based on the assumption that the back end logic on receipt of input creates 1 record per request and sends an email to the provided email address. Any logic to prevent this scenario by restricting multiple attempts originating from same ip address has not been observed during this test.
