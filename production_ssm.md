# Vulnerability Author
fatd0g

# Vulnerability Description
The plugin install functionality in the FastCms backend allows uploading malicious JAR packages, which can lead to arbitrary code execution (RCE)

# Vulnerability Type
Remote Code Execute

# Product Vendor
https://github.com/megagao/production_ssm
https://gitee.com/feng_ha_ha/ssm-erp

# Affected Product Code Repository
production_ssm

# Vulnerability Proof
## Code Analysis
The file upload function is implemented in the FileServiceImpl.java file, but it does not filter or process the file name. It directly concatenates the file name and the save path, which results in the ability to upload script files.
![image](https://github.com/user-attachments/assets/9679ea46-6598-4a75-990b-d1e0962e3b99)

Find the route that calls the uploadFile method in the FileController.java file
![image](https://github.com/user-attachments/assets/b9af9586-2f47-425a-95c4-25050943957a)

## Reproduction
Install the documentation, configure the database and tomcat server, and start the project

![image](https://github.com/user-attachments/assets/0c98d970-769f-44d2-a1ae-7b2ad4966564)

Log in to the backend to capture the package, directly connect the /file/upload route to upload the file
![image](https://github.com/user-attachments/assets/e75e8912-eb35-4d76-9b63-101de83178ab)

Access the path of the malicious plugin to execute arbitrary commands
![image](https://github.com/user-attachments/assets/a9ecd348-cfca-426f-b69a-8bd7b41c7f99)

# Code Location
src/main/java/com/megagao/production/ssm/service/impl/FileServiceImpl.java

# Repair Suggestions
Set a whitelist for uploaded file suffixes
