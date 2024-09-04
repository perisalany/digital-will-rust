
# Blockchain-Based Digital Will Management System

This project implements a decentralized will management system using Rust and the Internet Computer. The system allows users to manage wills, assets, beneficiaries, and executors in a secure and distributed manner. 

## Key Features

1. **User Management**
   - **Create User:** Allows users to create their profiles.
   - **Get User:** Retrieve details of a specific user.
   - **Get All Users:** Retrieve a list of all users in the system.

2. **Will Management**
   - **Create Will:** Allows users to create wills by assigning assets and beneficiaries.
   - **Get Will:** Retrieve a specific will by its ID.
   - **Get All Wills:** Retrieve a list of all wills in the system.

3. **Executor Management**
   - **Create Executor:** Create an executor to manage wills.
   - **Assign Executor:** Assign an executor to a will.
   - **Get Executor:** Retrieve details of a specific executor.
   - **Get All Executors:** Retrieve a list of all executors in the system.

4. **Asset Management**
   - **Add Asset:** Allows users to add assets to their wills.
   - **Get All Assets:** Retrieve a list of all assets within the system.

5. **Beneficiary Management**
   - **Add Beneficiary:** Allows users to assign beneficiaries to their wills.
   - **Get All Beneficiaries:** Retrieve a list of all beneficiaries in the system.

## Error Handling
- **Not Found:** Returns an error if a requested item (user, will, asset, etc.) is not found.
- **Unauthorized Access:** Returns an error if a user tries to perform an action without necessary permissions.

## Sample Payloads

### UserPayload

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

### WillPayload

```json
{
  "user_id": 1,
  "executor_id": 1
}
```

### AssetPayload

```json
{
  "will_id": 1,
  "name": "House",
  "value": 100000
}
```

### BeneficiaryPayload

```json
{
  "will_id": 1,
  "name": "Jane Doe",
  "share": 50
}
```

### ExecutorPayload

```json
{
  "name": "John Executor",
  "contact": "0734567890"
}
```

## Technologies Used

- **Rust:** For implementing logic and handling data structures.
- **Internet Computer (IC):** Decentralized infrastructure for managing persistent data.
- **Candid:** For serializing and deserializing data across the decentralized system.
- **ic_stable_structures:** For using stable structures in memory to store and retrieve data efficiently.

## Requirements

- rustc 1.64 or higher

```bash
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
$ source "$HOME/.cargo/env"
```

- rust wasm32-unknown-unknown target

```bash
$ rustup target add wasm32-unknown-unknown
```

- candid-extractor

```bash
$ cargo install candid-extractor
```

- install `dfx`

```bash
$ DFX_VERSION=0.15.0 sh -ci "$(curl -fsSL https://sdk.dfinity.org/install.sh)"
$ echo 'export PATH="$PATH:$HOME/bin"' >> "$HOME/.bashrc"
$ source ~/.bashrc
$ dfx start --background
```

If you want to start working on your project right away, you might want to try the following commands:

```bash
$ cd icp_rust_boilerplate/
$ dfx help
$ dfx canister --help
```

## Update dependencies

update the `dependencies` block in `/src/{canister_name}/Cargo.toml`:

```
[dependencies]
candid = "0.9.9"
ic-cdk = "0.11.1"
serde = { version = "1", features = ["derive"] }
serde_json = "1.0"
ic-stable-structures = { git = "https://github.com/lwshang/stable-structures.git", branch = "lwshang/update_cdk"}
```

## did autogenerate

Add this script to the root directory of the project:

```
https://github.com/buildwithjuno/juno/blob/main/scripts/did.sh
```

Update line 16 with the name of your canister:

```
https://github.com/buildwithjuno/juno/blob/main/scripts/did.sh#L16
```

After this run this script to generate Candid.
Important note!

You should run this script each time you modify/add/remove exported functions of the canister.
Otherwise, you'll have to modify the candid file manually.

Also, you can add package json with this content:

```
{
    "scripts": {
        "generate": "./did.sh && dfx generate",
        "gen-deploy": "./did.sh && dfx generate && dfx deploy -y"
      }
}
```

and use commands `npm run generate` to generate candid or `npm run gen-deploy` to generate candid and to deploy a canister.

## Running the project locally

If you want to test your project locally, you can use the following commands:

```bash
# Starts the replica, running in the background
$ dfx start --background

# Deploys your canisters to the replica and generates your candid interface
$ dfx deploy
```
