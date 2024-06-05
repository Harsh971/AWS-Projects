# Serverless CRUD Application

This project demonstrates the implementation of a serverless CRUD (Create, Read, Update, Delete) application using AWS services, including API Gateway, Lambda, and DynamoDB. The application allows users to manage data records stored in a DynamoDB table through RESTful API endpoints. Users can interact with the application using tools like Postman.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20APIGateway/Serverless%20CRUD%201/architecture.png"></img>

#### Project Architecture

- **API Gateway**: Acts as the entry point for all client requests. It routes HTTP requests to the appropriate Lambda functions.
- **AWS Lambda**: Contains the backend logic for handling CRUD operations. The Lambda function interacts with DynamoDB to perform the required operations.
- **DynamoDB**: A NoSQL database service that stores the data records.

#### Key Components

1. **API Gateway**: Configured to expose RESTful API endpoints for managing data in the DynamoDB table.
2. **Lambda Function**: A Python function that handles the logic for creating, reading, updating, and deleting items in the DynamoDB table.
3. **DynamoDB Table**: Stores the data records. Each item has a unique `id`, along with `name` and `value` attributes.

### How It Works

#### Setup

1. **API Gateway**: Defines the REST API with paths for each CRUD operation (`/items/{id}`).
2. **Lambda Function**: Implements the logic for each CRUD operation and is triggered by the API Gateway.
3. **DynamoDB Table**: Stores items with a primary key `id`.

#### template.yaml

```py
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Resources:
  DynamoDBTable:
    Type: 'AWS::DynamoDB::Table'
    Properties:
      TableName: 'ItemsTable'
      AttributeDefinitions:
        - AttributeName: 'id'
          AttributeType: 'S'
      KeySchema:
        - AttributeName: 'id'
          KeyType: 'HASH'
      ProvisionedThroughput:
        ReadCapacityUnits: 5
        WriteCapacityUnits: 5

  LambdaFunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: 'app.lambda_handler'
      Runtime: 'python3.9'
      CodeUri: .
      Environment:
        Variables:
          TABLE_NAME: !Ref DynamoDBTable
      Policies:
        - DynamoDBCrudPolicy:
            TableName: !Ref DynamoDBTable
      Events:
        ApiEvent:
          Type: Api
          Properties:
            Path: /items/{id}
            Method: ANY
            Cors:
              AllowMethods: "'GET,POST,PUT,DELETE,OPTIONS'"
              AllowHeaders: "'Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token'"
              AllowOrigin: "'*'"

Outputs:
  ApiUrl:
    Description: "API Gateway endpoint URL"
    Value: !Sub "https://${ServerlessRestApi}.execute-api.${AWS::Region}.amazonaws.com/Prod/items/{id}"

```

#### CRUD Operations

1. **Create (POST /items/)**
   - **Description**: Adds a new item to the DynamoDB table.
   - **Request**: Send a JSON body with `id`, `name`, and `value` attributes.
   - **Response**: Returns the created item.

2. **Read (GET /items/{id})**
   - **Description**: Retrieves a single item from the DynamoDB table by `id`.
   - **Request**: Provide the `id` of the item in the URL path.
   - **Response**: Returns the item with the specified `id`.

3. **Read All (GET /items/)**
   - **Description**: Retrieves all items from the DynamoDB table.
   - **Request**: No parameters required.
   - **Response**: Returns a list of all items.

4. **Update (PUT /items/{id})**
   - **Description**: Updates an existing item in the DynamoDB table.
   - **Request**: Provide the `id` in the URL path and a JSON body with `name` and `value` attributes.
   - **Response**: Returns the updated item.

5. **Delete (DELETE /items/{id})**
   - **Description**: Deletes an item from the DynamoDB table by `id`.
   - **Request**: Provide the `id` of the item in the URL path.
   - **Response**: Returns a status message indicating the outcome.

### Detailed Walkthrough

#### 1. **API Gateway Configuration**

The API Gateway is configured to handle HTTP requests for various CRUD operations:

- **Resource**: `/items/{id}`
- **Methods**: `GET`, `POST`, `PUT`, `DELETE`
- **CORS**: Enabled to allow cross-origin requests

#### 2. **Lambda Function (`app.py`)**

The Lambda function processes incoming requests and interacts with DynamoDB:

```python
import json
import boto3
from boto3.dynamodb.conditions import Key

dynamodb = boto3.resource('dynamodb')
table_name = 'ItemsTable'
table = dynamodb.Table(table_name)

def lambda_handler(event, context):
    http_method = event['httpMethod']
    path_parameters = event.get('pathParameters')
    body = event.get('body')

    if http_method == 'GET':
        if path_parameters:
            return get_item(path_parameters['id'])
        else:
            return get_all_items()
    elif http_method == 'POST':
        return create_item(json.loads(body))
    elif http_method == 'PUT':
        return update_item(path_parameters['id'], json.loads(body))
    elif http_method == 'DELETE':
        return delete_item(path_parameters['id'])
    else:
        return {
            'statusCode': 405,
            'body': json.dumps({'message': f'Unsupported method: {http_method}'})
        }

def get_item(item_id):
    try:
        response = table.get_item(Key={'id': item_id})
        if 'Item' not in response:
            return {'statusCode': 404, 'body': json.dumps({'message': 'Item not found'})}
        return {'statusCode': 200, 'body': json.dumps(response['Item'])}
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'message': str(e)})}

def get_all_items():
    try:
        response = table.scan()
        return {'statusCode': 200, 'body': json.dumps(response['Items'])}
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'message': str(e)})}

def create_item(item):
    try:
        table.put_item(Item=item)
        return {'statusCode': 201, 'body': json.dumps(item)}
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'message': str(e)})}

def update_item(item_id, item):
    try:
        response = table.update_item(
            Key={'id': item_id},
            UpdateExpression="set #name=:n, #value=:v",
            ExpressionAttributeNames={'#name': 'name', '#value': 'value'},
            ExpressionAttributeValues={':n': item['name'], ':v': item['value']},
            ReturnValues="ALL_NEW"
        )
        return {'statusCode': 200, 'body': json.dumps(response['Attributes'])}
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'message': str(e)})}

def delete_item(item_id):
    try:
        table.delete_item(Key={'id': item_id})
        return {'statusCode': 204, 'body': None}
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'message': str(e)})}
```

#### 3. **DynamoDB Table**

- **Table Name**: `ItemsTable`
- **Primary Key**: `id` (String)

### How to Use the Application

1. **Deploy the Application**
   - Use AWS SAM CLI to build and deploy the application.
   - Run the following commands:
     ```sh
     sam build
     sam deploy --guided
     ```
   - Follow the prompts to configure your stack name, AWS region, and other settings.

2. **Interact with the API**
   - Use Postman or any other API client to send HTTP requests to the API Gateway endpoints.

#### Example Requests in Postman

- **GET all items**
  - Method: GET
  - URL: `https://<API_ID>.execute-api.<REGION>.amazonaws.com/Prod/items/`
  - No body required

- **GET an item by ID**
  - Method: GET
  - URL: `https://<API_ID>.execute-api.<REGION>.amazonaws.com/Prod/items/{id}`
  - Replace `{id}` with the actual item ID

- **POST create a new item**
  - Method: POST
  - URL: `https://<API_ID>.execute-api.<REGION>.amazonaws.com/Prod/items/`
  - Body (JSON):
    ```json
    {
      "id": "1",
      "name": "ItemName",
      "value": "ItemValue"
    }
    ```

- **PUT update an item**
  - Method: PUT
  - URL: `https://<API_ID>.execute-api.<REGION>.amazonaws.com/Prod/items/{id}`
  - Replace `{id}` with the actual item ID
  - Body (JSON):
    ```json
    {
      "name": "UpdatedItemName",
      "value": "UpdatedItemValue"
    }
    ```

- **DELETE an item**
  - Method: DELETE
  - URL: `https://<API_ID>.execute-api.<REGION>.amazonaws.com/Prod/items/{id}`
  - Replace `{id}` with the actual item ID

This setup allows users to perform CRUD operations on the DynamoDB table through a simple, scalable serverless architecture. The API Gateway routes requests to the Lambda function, which executes the necessary logic to interact with DynamoDB.