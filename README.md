# Decentralized Voting System using Ethereum Blockchain

#### U2390827 - Usman Tariq - UEL - CN6035. A blockchain-powered voting DApp that ensures transparent, secure, and immutable elections. The system combines Ethereum smart contracts with a FastAPI backend and a MySQL database for user management.

#### For more details checkout Project Report at the home dir of this project.

## FEATURES
- JWT-based authentication for secure login and role-based access.
- Ethereum Smart Contracts ensure trustless, tamper-proof voting.
- Admin Dashboard for managing candidates, election dates, and results.
- User-friendly interface to vote and view candidates.

## Tools & Versions

| Tool        | Version / Info         |
|-------------|------------------------|
| Node.js     | 18.14.0                |
| Python      | 3.9                    |
| MetaMask    | Browser extension      |
| Ganache     | Local blockchain       |
| Truffle     | Global install         |
| MySQL       | Port 3306              |
| FastAPI     | Python backend         |

## DATABASE SETUP - MYSQL
Run MySQL server in Docker for ease and reliability.
  docker compose up -d

Update your .env file in Database_API:
  MYSQL_USER="root"
  MYSQL_PASSWORD="your_password"
  MYSQL_HOST="127.0.0.1"
  MYSQL_DB="voter_db"
  SECRET_KEY="your_super_secret_key / optional leave as is"

Login to mysql:
  mysql -h 127.0.0.1 -P 3306 -u root -p

Create the database and table in mysql:
  CREATE DATABASE voter_db;
  USE voter_db;
  CREATE TABLE voters (
    voter_id VARCHAR(36) PRIMARY KEY NOT NULL,
    role ENUM('admin', 'user') NOT NULL,
    password VARCHAR(255) NOT NULL
  );

Insert data use actual Ganache account addresses as voter_id.:
  INSERT INTO voters (voter_id, role, password) VALUES
  ('0x627306090abaB3A6e1400e9345bC60c78a8BEf57', 'admin', 'admin123'),
  ('0xf17f52151EbEF6C7334FAD080c5704D77216b732', 'user', 'voter123');

Navigate to the backend directory:
  cd Database_API

Create and activate virtual environment:
  python3 -m venv venv
  source venv/bin/activate

Install Python dependencies:
  pip install fastapi mysql-connector-python pydantic python-dotenv 'uvicorn[standard]' PyJWT

Start the FastAPI server for the mysql API:
  uvicorn main:app --reload --host 127.0.0.1

## BLOCKCHAIN SETUP
Install Ganache:
  npm install -g ganache

Start Ganache with deterministic accounts. this will store files in current directory to retain accounts:
  ganache --port 8545 --mnemonic "candy maple cake sugar pudding cream honey rich smooth crumble sweet treat" --networkId 5777

Add a custom network to MetaMask:
  Network Name: Localhost 8545
  RPC URL: http://127.0.0.1:8545
  Chain ID: 1337

Import a few test accounts from Ganache using the private keys shown in the CLI.
For production: Install Metamask for the browser and make a new wallet.

Install Truffle:
  npm install -g truffle

Compile and deploy the contracts:
  truffle compile
  truffle migrate --reset


## FRONTEND AND BACKEND SETUP
Setup - from root of the project:
  npm install

Bundle frontend code using Browserify:
  browserify ./src/js/app.js -o ./src/dist/app.bundle.js

Start the frontend server:
  node index.js

Visit the app in your browser:
  http://localhost:8080

## NOTES
Contract addresses change with each redeployment:
  truffle migrate --reset