============
AWS rollout
============

Camera system can be deployed on Amazon Web Services.


Requirements
===============================

AWS IAM User with following permissions

.. code-block:: json

    {}

Lambda
===============================

Create Lambda functions EvaluateMessage, ReceiveImage (set environment variable "TZ":"Europe/Berlin") and TelegramBot (create Layer with required dependencies) with roles assigned, permitted to use DynamoDB.


API Gateway
===============================

Create API as follows and integrate endpoints to Lambda functions. Roles allowed to use S3 must be assigned to endpoints:

.. code-block:: yaml

    ---
    swagger: "2.0"
    info:
      version: "2022-04-15T20:12:26Z"
      title: "<camera-system>"
    host: "<camera-system>"
    basePath: "/V1"
    schemes:
    - "https"
    paths:
      /ImageReceiver:
        x-amazon-apigateway-any-method:
          produces:
          - "application/json"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
      /images:
        post:
          produces:
          - "application/json"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
        options:
          consumes:
          - "application/json"
          produces:
          - "application/json"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
              headers:
                Access-Control-Allow-Origin:
                  type: "string"
                Access-Control-Allow-Methods:
                  type: "string"
                Access-Control-Allow-Headers:
                  type: "string"
      /images/{folder}/{object}:
        put:
          produces:
          - "application/json"
          parameters:
          - name: "object"
            in: "path"
            required: true
            type: "string"
          - name: "folder"
            in: "path"
            required: true
            type: "string"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
      /message:
        post:
          consumes:
          - "application/x-www-form-urlencoded"
          produces:
          - "application/xml"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
      /user/messages:
        get:
          produces:
          - "application/json"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
        post:
          consumes:
          - "application/x-www-form-urlencoded"
          produces:
          - "application/xml"
          responses:
            "200":
              description: "200 response"
              schema:
                $ref: "#/definitions/Empty"
    definitions:
      Empty:
        type: "object"
        title: "Empty Schema"


S3
===============================

Create S3 Bucket for images (trigger for Lambda function ReceiveImage for PUT) and artifacts.


DynamoDB
===============================

Create DynamoDB table.


Greengrass
===============================

Create Core Device, Component and Deployment (on Core Device) for IntervalSender. Use Artifact from S3 Bucket.
