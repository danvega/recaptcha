# Spring Security + Google reCaptcha 

I was asked in an episode of Spring Office Hours how they could perform reCaptcha verification using Spring Security. This
demo and the YouTube tutorial that goes with is my answer to that question.

## Google reCaptcha

To perform reCaptcha validation I am using [Google reCaptcha](https://www.google.com/recaptcha/about/) v3. You can use
the same approach used in this tutorial to plugin whatever verification service you would like to use. 

When you create a new reCaptcha service you will be given 2 keys, a site key and a secret key. Before you can run this
application you will need to add those keys to the configuration of this project. 

Site Key: src/frontend/.env
Secret Key: src/main/resources/application.properties

## Running the Application

You will need to open a terminal move into the `src/frontend` directory and run the following commands: 

```bash
npm install
npm run dev
```

Once the frontend application is running you can run the Spring Boot application with the following command: 

```bash
./mvnw spring-boot:run
```

## Tutorial

If you want to follow along with the tutorial you can checkout the `start-here` branch and watch the video below: 