# contoso-air

## Prerequisites

- Node.js 22.0.0 or later

## Getting Started

Create an Azure CosmosDB account and export the account name and access key as environment variables:

```bash
RAND=$RANDOM
export RAND
echo "Random resource identifier will be: ${RAND}"

LOCATION=eastus
RG_NAME=rg-contosoair$RAND
DB_NAME=db-contosoair$RAND

az group create \
  --name $RG_NAME \
  --location $LOCATION

az cosmosdb create \
  --name $DB_NAME \
  --resource-group $RG_NAME \
  --kind MongoDB

az identity create \
  --name db-contosoair$RAND-id \
  --resource-group $RG_NAME

export COSMOS_DB_AUTH_KEY=$(az cosmosdb keys list --name $DB_NAME --resource-group $RG_NAME --query primaryMasterKey -o tsv)
export COSMOS_DB_URL=$DB_NAME.mongo.cosmos.azure.com:10255
export COSMOS_DB_DATABASE=contosoair
```

Clone the repository then run the following commands:

```bash
# change directory
cd src/web

# install dependencies
npm install

# run the app
npm start
```

Browse to `http://localhost:3000` to see the app.

## Running with Docker

### Using Docker

Build and run the application using Docker:

```bash
# Build the Docker image
docker build -t contoso-air .

# Run the container
docker run -p 3000:3000 contoso-air

# Run with Azure CosmosDB (optional)
docker run -p 3000:3000 \
  -e COSMOS_DB_AUTH_KEY=your-auth-key \
  -e COSMOS_DB_URL=your-cosmos-db-url \
  -e COSMOS_DB_DATABASE=contosoair \
  contoso-air
```

### Using Docker Compose

Run the application using Docker Compose:

```bash
# Start the application
docker-compose up

# Start in detached mode
docker-compose up -d

# Stop the application
docker-compose down
```

To configure Azure CosmosDB, edit the `docker-compose.yml` file and uncomment the environment variables.

Browse to `http://localhost:3000` to see the app.
