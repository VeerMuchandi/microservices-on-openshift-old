> This repo demos usage of  microservices on open-shift.  
> Microservices created in different languages communicate over REST as per picture below

![alt tag](https://raw.githubusercontent.com/debianmaster/microservices-on-openshift/master/Arch.png)

## for mongodb
```sh
oc new-app -e \
    MONGODB_USER=app_user,MONGODB_PASSWORD=password,MONGODB_DATABASE=sampledb,\
    MONGODB_ADMIN_PASSWORD=admin_pass \
    registry.access.redhat.com/rhscl/mongodb-26-rhel7
```
## for python email-api 

```sh
oc new-app debianmaster/python-email-api  
oc expose dc/python-email-api --port 8080  
oc expose svc/python-email-api   
```

## for php-ui 
```sh
oc new-app --context-dir='php-ui' https://github.com/debianmaster/microservices-on-openshift.git   
oc env dc/php-ui NODEJS_APPLICATION_DOMAIN=http://nodejs-users-api-microservices.apps.osecloud.com  
```

## for nodejs-users-api
```sh
oc new-app --context-dir='nodejs-users-api' https://github.com/debianmaster/microservices-on-openshift.git  
oc env dc/nodejs-users-api MONGODB_DATABASE=sampledb MONGODB_PASSWORD=password MONGODB_USER=app_user  MONGODBDATABASE_SERVICE_NAME=mongodb PYTHON_APPLICATION_DOMAIN=http://python-email-api-microservices.apps.osecloud.com
```
