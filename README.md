
![Uni BA](https://user-images.githubusercontent.com/9687840/143562844-d50cb825-4279-489f-90ed-01e0db0ef2ef.png)

Pre-requisites
1. Download and install WSO2 API Manager 4 (zip distribution used here) https://apim.docs.wso2.com/en/latest/install-and-setup/install/installing-the-product/installing-api-m-runtime/

2. Download and install RabbitMQ and MySQL
3. Download and install WSO2 Micro Integrator (https://apim.docs.wso2.com/en/4.0.0/install-and-setup/install/installing-the-product/installing-mi) 
4. In MYSQL create a user with credentials user1/user1 and necessary permissions
4. Execute the studentsdbscript file in MySQL that would create the relevant DB and table. 

Deploy artifacts 

1. Add (StudentRegistration) car file  into <MI_HOME>/repository/depoyment/server/carbonapps folder
2. Add below configurations to <MI_HOME>/repository/conf/deployment.toml file 
 [transport.rabbitmq]
sender_enable = true

[[service_catalog]]
apim_host = "https://localhost:9443"
enable = true
username = "admin"
password = "admin"

3. Add mysql-connector-java-8.0.19.jar and amqp-client-5.7.0.jar to <MI_HOME>/libs folder

4. Start the API Manager server as explained in https://apim.docs.wso2.com/en/latest/install-and-setup/install/installing-the-product/running-the-api-m/

5. Start WSO2 Micro Integrator as explained in https://apim.docs.wso2.com/en/latest/install-and-setup/install/installing-the-product/running-the-mi/

6. Once the MI server starts and the service is deployed login to the API Publisher portal ( 9443 ,admin/admin) and go to Service Catalog tab to locate the deployed service.

7. Create an API from this service similar to  https://apim.docs.wso2.com/en/latest/design/create-api/create-an-api-using-a-service/#step-2-discover-the-services   


Sample Invocations 

[GET] Student Registration Details
http://localhost:8290/course/register/student/1100
Accept: application/json

[POST] Add new student registration
Content-Type: application/json
{
"StudentNumber":"1200",
"FirstName":"Alexis",
"LastName":"Parker",
"Email":"alexisp@unih.com",
"Modules":"Communication Skills"
}

You can access RabbitMQ console(  http://localhost:15672 ,   guest/guest credentials by default) and see the queue getting populated.
