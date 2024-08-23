# Splunk-2-100-series-questions


## Project Report: Investigation of HTTP and SMTP Traffic Using Splunk

### 1. Overview

In this project, I focused on investigating HTTP and SMTP traffic logs to uncover specific details related to a potential competitor investigation. The analysis was conducted using Splunk, with a series of queries designed to filter and extract the necessary information. The process involved identifying key data points such as website domains, image file paths, email addresses, and file attachments. This project also required decoding base64 data using CyberChef to retrieve hidden information.

### 2. Objectives

The primary objective of this investigation was to find out the following:

    The competitor website that was visited.
    The image file displaying executive contact information.
    The name and email address of the competitor's CEO.
    The email address of another employee at the competitor contacted by Amber.
    The name of the file attachment Amber sent to a contact at the competitor.
    Amber's personal email address.

### 3. Methodology

Identifying Amber’s IP Address:

![image](https://github.com/user-attachments/assets/16242851-f3b5-4c43-9070-e9b913fd8734)

The investigation began by querying Splunk to find Amber’s IP address using the following query:

    index="botsv2" sourcetype="pan:traffic" amber

    Amber's IP address was identified as 10.0.2.101.

### 1. Finding the Competitor Website:

#### Question: What is the website domain that Amber visited?

    
  ![image](https://github.com/user-attachments/assets/dc7ebd38-7497-4c9d-a2f5-b5c9c72a25cc)
  
![image](https://github.com/user-attachments/assets/e7338649-28c7-4514-b590-d0e669b8c639)

  ![image](https://github.com/user-attachments/assets/78cf75b3-f823-4634-8fd0-829456524fdc)
  
  ![image](https://github.com/user-attachments/assets/06c65deb-7f1d-4c9e-8d6f-7f1b6de7e029)
    
   
    
To find the website Amber visited, I refined the query to focus on HTTP traffic:

    index="botsv2" sourcetype="stream:HTTP" "10.0.2.101" 
    | dedup site 
    | table site

  The site www.berkbeer.com was identified as the competitor’s website.

### 2. Locating the Image File:

  #### Question: What image file displayed the executive’s contact information?
  
   I then searched for the image file that displayed the CEO’s contact information using:

   ![image](https://github.com/user-attachments/assets/caaf1247-1273-42ee-ba7d-6e5eaf66443f)



    index="botsv2" sourcetype="stream:HTTP" "10.0.2.101" berkbeer.com

  The file path was identified as /images/ceoberk.png.

### 3. Identifying the CEO’s Name and Email:

  Question: What is the CEO’s name? Provide the first and last name.
  
  ![image](https://github.com/user-attachments/assets/e3d96eed-dfdf-40fa-9b49-40574f066448)
  
 ### 4. Question: What is the CEO’s email address?
   Switching to SMTP traffic, I used the following query to find the CEO’s email communications:

  


    index="botsv2" sourcetype="stream:smtp" berkbeer.com

    The CEO’s name was found to be Martin Berk, and his email address was mberk@berkbeer.com.

Finding the Employee's Email:

  ### 5. Question: What is the email address of another employee contacted by Amber?

   ![image](https://github.com/user-attachments/assets/18e8f287-64a8-44ea-8a29-91cec27bde8f)

  The search revealed another employee, and the query was refined to include Amber’s email:


        index="botsv2" sourcetype="stream:smtp" berkbeer.com "aturing@froth.ly"

  The email address of the employee contacted by Amber was identified as hbernhard@berkbeer.com.

  ### Finding the File Attachment:
  ### 6. Question: What is the name of the file attachment that Amber sent to a contact at the competitor?
  
  The file attachment was located using Splunk’s “Interesting Fields” feature:
      The attachment name was Saccharomyces_cerevisiae_patent.docx.

### 7. Decoding Amber's Personal Email:
  ### Question: What is Amber’s personal email address?
  
  Amber’s personal email was hidden in base64-encoded data. Using CyberChef, I decoded the data to find:

  ![image](https://github.com/user-attachments/assets/0c3dbc8e-fa14-451f-ab01-2d6e05743d80)

![image](https://github.com/user-attachments/assets/7c60ba0f-c869-47de-a2ee-4af44f945c7d)


            The email address was ambersthebest@yeastiebeastie.com.

4. Challenges

During the investigation, several challenges were encountered, such as:

  Identifying Keywords and Filters: I had to ensure that the correct keywords and filters were applied to accurately extract the necessary data.
  Decoding Base64 Data: Retrieving Amber's personal email required decoding base64 data, which involved careful analysis and the use of external tools like CyberChef.

5. Conclusion

This project highlighted the importance of meticulous log analysis and the application of correct search queries in Splunk to uncover critical information. Through this investigation, I was able to successfully identify key data points related to the competitor investigation, including websites visited, email communications, and file attachments. This exercise reinforced my skills in using Splunk for log analysis and my ability to decode and analyze encoded data.

This report demonstrates my ability to conduct thorough investigations using Splunk and related tools, applying both technical skills and problem-solving strategies to achieve the objectives.
